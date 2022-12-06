<template>
  <div id="header">MedForum Movie Night List</div>
  <div v-for="(movie, index) in movies" :key="index" class="movieContainer">
    <div class="center">
      <h3>{{ movie.name }}</h3>
      <p class="duration">{{ movie.duration }}</p>

      <button @click="toggle(movie.id)" class="watchBtn">
        <p v-show="!movie.open">►</p>
        <p v-show="movie.open">▼</p>
      </button>
    </div>
    <div v-if="movie.open">
      <video controls="controls" autoplay name="media">
        <source
          :src="require(`@/assets/movie${index + 1}.mp4`)"
          alt="video"
          type="video/mp4"
          width="500px"
          autoplay
        />
      </video>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      movies: [
        {
          name: "Windy Highway",
          duration: "15 seconds",
          open: false,
          id: 1,
          movieStart: "0:00",
          movieMid: "0.08",
          movieEnd: "0:15",
        },
        {
          name: "Sunny Station",
          duration: "32 seconds",
          open: false,
          id: 2,
          movieStart: "0:00",
          movieMid: "0.16",
          movieEnd: "0:32",
        },
        {
          name: "Abstract Material",
          duration: "9 seconds",
          open: false,
          id: 3,
          movieStart: "0:00",
          movieMid: "0.05",
          movieEnd: "0:09",
        },
        {
          name: "Pumpkin Drilling",
          duration: "17 seconds",
          open: false,
          id: 4,
          movieStart: "0:00",
          movieMid: "0.09",
          movieEnd: "0:17",
        },
      ],
    };
  },
  methods: {
    toggle(id) {
      const state = this.movies[id - 1].open;
      this.movies.forEach((movie) => (movie.open = false));
      this.movies[id - 1].open = !state;

      console.log(
        this.movies[id - 1].movieStart,
        "-",
        this.movies[id - 1].movieMid,
        "-",
        this.movies[id - 1].movieEnd
      );
    },
  },
};
</script>

<style lang="scss">
$primaryColor: #2c3e50;
$primaryBtnColor: red;
$btnHoverColor: rgb(255, 191, 107);

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $primaryColor;
  margin: 0 auto 0;
}
#header {
  background-color: $primaryColor;
  padding: 15px 0;
  color: white;
}
.watchBtn {
  background-color: $primaryBtnColor;
  border-radius: 10px;
  margin-left: 10px;
  height: 20px;
  display: flex;
  align-items: center;
  &:hover {
    background-color: $btnHoverColor;
    cursor: pointer;
  }
}

.movieContainer {
  margin: 5px auto;
  display: flex;
  flex-direction: column;
  video {
    width: 500px;
  }
}
.center {
  margin: 0 auto;
  display: flex;
  align-items: center;
}
.duration {
  margin: 0 5px 0 10px;
}
</style>
