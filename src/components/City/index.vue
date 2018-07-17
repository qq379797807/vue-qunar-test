<template>
  <div class="wrapper">
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list
      :cities="cities"
      :hot="hotCities"
      :letter="letter"
    ></city-list>
    <city-alpha @changeLetter="changeLetter"
      :cities="cities"
    ></city-alpha>
  </div>
</template>

<script>
import CityHeader from './Header'
import CitySearch from './Search'
import CityList from './List'
import CityAlpha from './Alhpabet'
import axios from 'axios'

export default {
  name: 'City',
  components: {
    CityHeader, CitySearch, CityList, CityAlpha
  },
  data () {
    return {
      hotCities: [],
      cities: null,
      letter: null
    }
  },
  mounted () {
    this.getCityInfo()
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.getCityInfoSucc)
    },
    getCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    changeLetter (letter) {
      this.letter = letter
    }
  }
}
</script>

<style lang="stylus" scoped>

</style>
