<template>
  <div class="movie">
    <h1>{{movie.name}}</h1>
    <img v-bind:src="movie.poster" alt="poster" class="poster">
    <p>
        감독 : {{movie.director}}<br>
        출연 : {{movie.actors}}<br>
        러닝타임 : {{movie.time}}<br>
    </p>
    <h2>줄거리</h2>
    <p v-html="movie.synopsis" class="synopsis">
    </p>
    <router-link :to="{name: 'index'}">돌아가기</router-link> <!--인덱스페이지로 돌아감-->
  </div>
</template>

<script>
export default {
  created: function () {
    var id = this.$route.params.id
    this.$http.get(`/api/movies/${id}`)
    .then((response) => {
      console.log(response.data)
      this.movie = response.data[0]

    })
  },
  data: function () {
    return {
      movie: {}
    }
  }
}
</script>