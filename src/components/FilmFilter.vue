<template>
    <div class="film-filter">
        <span>Filter:</span>
        <button @click="changeSortType('year')" class="film-filter__button"
            :class="sortType === 'year' ? 'film-filter__button--active' : ''">Year</button>
        <button @click="changeSortType('title')" class="film-filter__button"
        :class="sortType === 'title' ? 'film-filter__button--active' : ''">Title</button>
    </div>
</template>

<script>

import {inject} from "vue";

export default {
    name: "Film Filter",
    setup(){
        const sortType = inject("sortType");
        const changeSortType = (type) => {
            sortType.value = type;
        }
        return {
            changeSortType,
            sortType
        }
    }
}

</script>

<style scoped>
    .film-filter {
        display: flex;
        padding: 2rem 1rem 0.5rem 1rem;
        gap: 0.5rem;
    }
    .film-filter__button {
        border: none;
        padding:0.5ch 1.5ch;
        border-radius:2ch;
    }
    .film-filter__button--active {
        /* box-shadow: 0 0 0.25rem hsla(0, 0%, 0%, 0.5) inset; */
        background: hsl(0, 0%, 60%);
        color: #fff;
    }
</style>