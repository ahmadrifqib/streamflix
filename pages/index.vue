<template>
  <div>
    <NavigationBar/>
    <div>Hello World {{ tes }}</div>

    <ul id="movieList">
      <li v-for="item in movieResponse" :key="item.title">
        <h1>Nama film: {{ item.title }}</h1>
        <h2>Rating: {{ item.vote_average }}</h2>
        <h2>Harga nonton: Rp{{ item.price }}</h2>
        <button>Detail</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
// const API_KEY = 'bf52d2c3591ad0262391d3a327082756'

export default Vue.extend({
  data() {
    return {
      tes: 'Tes Film',
      currentPage: 1,
      movieResponse: [
        {
          title: 'tes',
          vote_average: -1,
          price: -1,
        },
      ],
    }
  },
  mounted() {
    localStorage.setItem('balance', '100000')
    // TODO:
    // 1. PASANG UI LIBRARY & PAGINATION
    // 2. BUAT FILE BARU UNTUK PAGE DETAIL
    // 3. NAVIGASI PAKAI BUTTON & PASSING OBJECT ITEM FILM KE PAGE DETAIL
    // 4. TAMPILIN DUIT DAN GUNAIN LOCALSTORAGE BUAT BELI FILM
    // TIAP PAGE ADA 20 ITEMS
    this.$axios
      .get(
        `https://api.themoviedb.org/3/discover/movie/?api_key=bf52d2c3591ad0262391d3a327082756&page=${this.currentPage}`
      )
      .then((response) => {
        this.movieResponse = response.data.results
        console.log('MOVIE RESPONSE')
        console.log(response.data)

        this.movieResponse = this.movieResponse.map((i) => {
          let price = 0

          if (i.vote_average < 4) {
            price = 3_500
          } else if (i.vote_average < 6) {
            price = 8_250
          } else if (i.vote_average < 8) {
            price = 16_350
          } else {
            price = 21_250
          }

          return {
            title: i.title,
            vote_average: i.vote_average,
            price,
          }
        })
      })
  },
})
</script>
