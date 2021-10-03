<template>
  <div class="antialiased">
    <NavigationBar />
    <div class="container mx-auto py-3">
      <div class="d-flex flex-column align-items-center">
        <div class="d-flex justify-content-center">
          <ul class="row">
            <li
              v-for="item in movieResponse"
              id="movieList"
              :key="item.title"
              :per-page="perPage"
              :current-page="currentPage"
              style="list-style-type: none"
              class="col p-4"
            >
              <a :href="'/movie/' + item.id" class="card" style="width: 18rem">
                <img :src="item.imageUrl" class="card-img-top" />
                <div class="card-body">
                  <h5 class="card-title">{{ item.title }}</h5>
                  <!-- <p class="card-text">
                  {{ item.overview }}
                </p> -->
                </div>
                <ul class="list-group list-group-flush">
                  <!-- <li class="list-group-item">An item</li> -->
                  <li class="list-group-item">
                    Rating: {{ item.vote_average }}
                  </li>
                  <li class="list-group-item">
                    Harga nonton: Rp{{ item.price }}
                  </li>
                </ul>
                <!-- <div class="card-body">
                <a href="#" class="card-link">Card link</a>
                <a href="#" class="card-link">Another link</a>
              </div> -->
              </a>
            </li>
          </ul>
        </div>
        <div class="d-flex justify-content-center">
          <b-pagination
            v-model="currentPage"
            :total-rows="rows"
            :per-page="perPage"
            first-text="First"
            prev-text="Prev"
            next-text="Next"
            last-text="Last"
            aria-controls="movieList"
          ></b-pagination>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue"
// const API_KEY = 'bf52d2c3591ad0262391d3a327082756'

export default Vue.extend({
  data() {
    return {
      tes: "Tes Film",
      currentPage: 1,
      movieResponse: [
        {
          id: 0,
          title: "",
          overview: "",
          vote_average: -1,
          imageUrl: "",
          price: -1,
        },
      ],
    }
  },
  computed: {
    rows() {
      return this.movieResponse.length
    },
  },

  mounted() {
    localStorage.setItem("balance", "100000")
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
        // this.moviePageTotal = response.data
        this.movieResponse = response.data.results
        // console.log("MOVIE RESPONSE")
        // console.log(response.data)

        this.movieResponse = this.movieResponse.map((i) => {
          let price = 0
          const imageUrl = "https://image.tmdb.org/t/p/original/"

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
            id: i.id,
            title: i.title,
            overview: i.overview,
            vote_average: i.vote_average,
            imageUrl: imageUrl + i.backdrop_path,
            price,
          }
        })
      })
  },
})
</script>
