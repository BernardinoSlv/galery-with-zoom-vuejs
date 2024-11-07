<template>
    <div class="row row-cols-1 row-cols-md-2 row-cols-xl-3 g-3">
        <template v-for="image in images" :key="image.id">
           <Image :image="image" />
        </template>
    </div>
</template>

<script setup>
import Image from './Image.vue';

defineProps(['images'])

</script>