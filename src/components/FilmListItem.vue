<template>
    <div class="list-item">
        <h3 class="list-item__title">{{filmTitle}}</h3>
        <img :src="imageUrl" class="list-item__img" />
    </div>
</template>


<script>

export default {
    props: {
        filmTitle : { default: "Film Title", type: String },
        imageUrl : { default : "", type: String }
    },
    setup(){

    }
}
</script>


<style scoped>
.list-item {
    cursor: pointer;
    margin:1rem;
    padding:1rem;
    box-shadow: 0 0.1rem 0.4rem 0 hsla(0, 0%, 0%, 0.2);
    border-radius: 0.5rem;
}

.list-item__title {
    margin-top: 0;
}

.list-item__img {
    display: block;
    width: 100%;
    height: auto;
}
</style>
