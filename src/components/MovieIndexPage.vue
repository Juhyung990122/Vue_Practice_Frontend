<template>
<div class="movies">
    <h1>영화 목록</h1>
    <div class="movie" v-for="(movie) in movies" :key="movie" ><!--키속성을 설정하여 동적 값에 바인딩 해야함(데이터 간단하면 생략)-->
      <img v-bind:src="movie.poster" class="poster">
      <div>
        <strong>{{movie.name}}</strong>
        <br>
        <p>
          {{movie.director}}
          <br>
          예매율: {{movie.rate}}
        </p>
        <router-link :to="{ name: 'show', params: { id: movie.id }}">더보기</router-link> <!--누르면 라우터객체를 통해 디테일로 들어감, id를 파라미터로 넘겨줌-->
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  created () {      
    this.$http.get(`/api/movies`) //여기수정
        .then((response) => {
          this.movies = response.data //movie에 response의 data를 넣음.
        })
  },
  data () {
    return {
      movies: []
    }
  }
}
</script>
