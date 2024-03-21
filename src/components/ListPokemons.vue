<script setup>
import { defineProps } from 'vue';

const props = defineProps(['nome', 'urlImage']);

</script>
<template>
    <div class="col-md-4">
        <div class="card style-card mb-3 p-2">
            <p class="text-center">{{ props.nome }}</p>
            <img
                :src="urlImage"
                class="card-img-top"
                alt="..."
                height="80"
                />
        </div>
    </div>
</template>

<style scoped>

.style-card{
    background: rgb(63,240,251);
    background: radial-gradient(circle, rgba(63,240,251,0.7707457983193278) 58%, rgba(5,255,80,0.4654236694677871) 100%);
    transition: easy-out 0.3s;
    cursor: pointer;
}

.style-card:hover{
    background: rgb(63,240,251);
    background: radial-gradient(circle, rgba(63,240,251,1) 58%, rgba(5,255,80,0.4654236694677871) 100%);
    transition: easy-out 0.3s;
}

.style-card:hover img{
    padding: .1rem;
}
</style>