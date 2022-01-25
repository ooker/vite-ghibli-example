<template>
    <div class="film-info">
        <div class="film-info__image">
            <img :src="imageUrl" class="film-info__img" />
        </div>
        <div class="film-info__data">
            <main>
                <h2>{{filmTitle}} <span class="film-info__year">{{releaseDate}}</span></h2>
                <p>{{filmDescription}}</p>
            </main>
            
            <footer class="film-info__prevnext">
                <prev-next-buttons />
            </footer>
        
        </div>
    </div>
</template>


<script>

import PrevNextButtons from "./PrevNextButtons.vue";

export default {
    props: {
        filmTitle : String,
        filmDescription : String,
        imageUrl : String,
        releaseDate : String
    },
    components : {
        PrevNextButtons
    }
}
</script>


<style scoped>

.film-info {
    display: flex;
}
.film-info__img {
    display: block;
    height: 100vh;
    width: auto;
}

.film-info__data {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 100vh;
    padding: 2vw;
}
.film-info__year {
    font-size:64%;
    font-weight: normal;
    font-style: italic;
    vertical-align: super;
}
.film-info__prevnext {
    /* align-self: flex-end; */
    justify-self: flex-end;
}
</style>
