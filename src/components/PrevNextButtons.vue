<template>
    <div class="prevnext">
        <button @click="prevNext('prev')">Previous</button>
        <button @click="prevNext('next')">Next</button>
    </div>
</template>

<script>

import {inject} from "vue";

export default {
    setup(){
        const active = inject("active");
        const prevNext = (direction) => {
            if(direction === "prev"){
                active.value--;
            } else if (direction === "next"){
                active.value++;
            } 
        }
        return {
            active,
            prevNext
        }
    }
}
</script>

<style scoped>
.prevnext {
    display: flex;
    justify-content: flex-end;
    gap: 0.5rem;
}
</style>