<template>
  <div v-if="filmsData" class="films">
    <div class="films-list">
      <FilmFilter />
      <FilmListItem v-for="(film, i) in sortedData" :key="film.id" 
      :filmTitle="film.title" :imageUrl="film.movie_banner"
      @click="listItemClick(i)" />
    </div>
    <div class="films-info">
      <FilmInfo
        v-if="active!=null" 
        :filmTitle="sortedData[active].title" 
        :imageUrl="sortedData[active].image" 
        :filmDescription="sortedData[active].description"
        :releaseDate="sortedData[active].release_date"
      />
    </div>
  </div>
</template>



<script>
import { ref, provide, computed } from 'vue';
import FilmListItem from "./components/FilmListItem.vue";
import FilmInfo from "./components/FilmInfo.vue";
import FilmFilter from "./components/FilmFilter.vue";

export default {
  components : {
    FilmListItem,
    FilmInfo,
    FilmFilter
  },
  setup(){
    const filmsData = ref(null);
    const active = ref(null);
    const sortType = ref("title");

    fetch('https://ghibliapi.herokuapp.com/films')
    .then(response => response.json()).then(data => filmsData.value = data);

    const listItemClick = (idx) => {
      active.value = idx;
    } 

    const sortedData = computed(() => {
      switch (sortType.value){
        case "year":
          return [...filmsData.value].sort( (a, b) => {
            return a.release_date.localeCompare(b.release_date);
          });
        case "title":
          return [...filmsData.value].sort( (a, b) => {
            return a.title.localeCompare(b.title);
          });
      } 
    });


    provide("sortType", sortType);
    provide("active", active);

    return {
      filmsData,
      sortedData,
      active,
      listItemClick
    }

  }
}
</script>

<style>
html {box-sizing: border-box;}
*, *::before, *::after {
  box-sizing: inherit;
}
body {
  margin: 0; 
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.films {
  display: flex;
  flex-direction: row;
  height: 100vh;
}
.films-list {
  flex-grow: 1;
  flex-basis: clamp(16rem, 25vw, 30rem);
  overflow-y: scroll;
}

.films-list::-webkit-scrollbar {
  width: 5px;
  height: 8px;
  background-color: #aaa; 
}
.films-list::-webkit-scrollbar-thumb {
    background: #000;
}
.films-info {
  flex-grow: 1;
  flex-basis: clamp(48rem, 75vw, 96rem);
}


</style>
