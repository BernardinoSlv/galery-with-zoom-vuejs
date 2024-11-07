<template>
    <h1>Galeria de imagens</h1>
    <div class="input-group input-group-lg border-bottom border-3 pb-2 mb-3">
        <input type="text" class="form-control" placeholder="https://site.com/image.jpg" ref="inputRef" v-on:keydown.enter="add">
        <button class="btn btn-primary" @click="add">Adicionar</button>
    </div>

    <Collection :images="images" />
</template>

<script setup>
import Collection from "./Collection.vue"
import {ref, useTemplateRef, provide} from "vue"

const inputRef = useTemplateRef('inputRef')
const images = ref([])

provide('imagesFunc', {
    remove
})

function remove(id) {
    if (!confirm('Exluir imagem ?'))
        return
    images.value = images.value.filter(item => item.id !== id)
}

function add() {
    const url = inputRef.value.value.trim()

    // validações
    if (!url.length)
        return
    else if (images.value.find((image) => image.url === url)) {
        alert("Já está no album")
        inputRef.value.value = ""
        return
    }

    images.value.push({
        id: images.value.length,
        url
    })

    inputRef.value.value = ""
}

</script>