<template>
     <div class="col" >
        <div class="card shadow">
            <div class="card-body "  style="height: 250px;">
                <div ref="container-image"
                    class="h-100 w-100 container-image position-relative" 
                    :class="{
                        'in-zoom': inZoom
                    }"
                    :style="[`background-image: url('${image.url}')`]"
                    @mousemove.self="move"
                    @mouseenter="inFocus = true"
                    @mouseleave="inFocus = false"
                >
                    <div class="position-absolute translate-middle top-50 start-50 d-flex gap-2" :class="{
                        'd-none': !inFocus
                    }">
                        <button class="btn btn-primary" @click="inZoom = !inZoom">
                            <i class="bi" :class="{
                                'bi-zoom-out': inZoom,
                                'bi-zoom-in': !inZoom
                            }"></i> 
                        </button>
                        <button class="btn btn-danger" @click="remove(image.id)">
                            <i class="bi bi-trash-fill"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {ref, inject, useTemplateRef} from "vue"

defineProps(['image'])

const containerImage = useTemplateRef('container-image')
const inFocus = ref(false)
const inZoom = ref(false)
const {remove} = inject('imagesFunc')

function move(event) {
    if (!inZoom.value)
        return

    const {layerX, layerY} = event
    const {clientWidth, clientHeight} = containerImage.value

    const backgroundPositionX = Math.round((100 / clientWidth) * layerX)
    const backgroundPositionY = Math.round((100 / clientHeight) * layerY)

    containerImage.value.style.backgroundPositionX = backgroundPositionX + "%"
    containerImage.value.style.backgroundPositionY = backgroundPositionY + "%"

    console.log(backgroupPositionX + "%", backgroupPositionY + "%")
}
</script>

<style scoped>
    .container-image {
        object-fit: cover;
        background-position: center;
        background-size: contain;
        background-repeat: no-repeat;
    }

    .in-zoom {
        background-size: 400%;
    }
</style>