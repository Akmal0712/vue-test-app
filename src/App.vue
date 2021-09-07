<template>
  <div id="app">
    <l-map style="height: 900px" :zoom="zoom" :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker v-for="item in items" :lat-lng="[item.latitude, item.longitude]" :key=item.id>
        <l-tooltip :options="{ permanent: true, interactive: true }">{{ item.name }}</l-tooltip>
      </l-marker>
    </l-map>
    <div class="navbar">
      <h3>Объекты</h3>
      <label for="search">Поиск</label>
      <input type="text" v-model="search" id="search"/>
      <p v-for="item in filteredItems" :key="item.id" @click="changeCenter(item)">{{ item.name }}</p>
    </div>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LTooltip } from 'vue2-leaflet'

export default {
  name: 'App',
  components: {
    LMap,
    LMarker,
    LTileLayer,
    LTooltip
  },
  data () {
    return {
      search: '',
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
          '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 5,
      center: [50.760918, 4.110170],
      markerLatLng: [50.760918, 4.110170],
      filteredItems: [],
      items: [
        {
          "id": 1,
          "latitude": 50.760918,
          "longitude": 4.110170,
          "name": "ВАЗ"
        },
        {
          "id": 2,
          "latitude": 47.492647,
          "longitude": 19.051399,
          "name": "ГАЗель"
        },
        {
          "id": 3,
          "latitude": 41.902689,
          "longitude": 12.496176,
          "name": "Lexus"
        },
        {
          "id": 4,
          "latitude": 43.779787,
          "longitude": 11.265817,
          "name": "Volkswagen"
        },
        {
          "id": 5,
          "latitude": 52.373057,
          "longitude": 4.892557,
          "name": "Lada"
        },
        {
          "id": 6,
          "latitude": -22.903150,
          "longitude": -43.189903,
          "name": "Kia"
        },
        {
          "id": 7,
          "latitude": 38.716174,
          "longitude": -9.141589,
          "name": "Bentley"
        },
        {
          "id": 8,
          "latitude": 50.080293,
          "longitude": 14.428983,
          "name": "Porsche"
        },
        {
          "id": 9,
          "latitude": 48.856663,
          "longitude": 2.351556,
          "name": "BMW"
        },
        {
          "id": 10,
          "latitude": 45.438095,
          "longitude": 12.319029,
          "name": "Honda"
        }
      ]
    }
  },
  watch: {
    search() {
      if (!this.search)
        return this.filteredItems = this.items

      this.filteredItems = this.items.filter(item => (item.name.toUpperCase()).includes(this.search.toUpperCase()))
    }
  },
  created() {
    this.filteredItems = this.items
  },
  methods: {
    changeCenter(item) {
      this.center = [item.latitude, item.longitude]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.navbar {
  width: 250px;
  height: 80%;
  background-color: white;
  position: absolute;
  top: 100px;
  right: 100px;
  z-index: 1000;
}

p {
  line-height: 2;
  text-align: left;
  padding-left: 15px;
}
p:hover {
  background-color: aliceblue;
}
</style>
