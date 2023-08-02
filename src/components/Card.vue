<script setup>
import { computed } from 'vue'

const props = defineProps({
    position: {type: Number, required: true},
    value   : {type: String, required: true},
    visible : {type: Boolean, default: false},
    matched : {type: Boolean, default: false}
})
const emit = defineEmits(['select-card'])
const flippedStyles = computed(() => {
    if(props.visible) {
        return 'is-flipped'
    }
})
const selectCard = () => {
    emit('select-card', {
        position:  props.position,
        faceValue: props.value
    })
}

</script>

<template>
    <div class="card" :class="flippedStyles" @click="selectCard">
        <div class="card-face is-front">
            <img
            :src="`/images/${props.value}.png`"
            :alt="props.value" />
            <img v-if="props.matched"
            src="/images/checkmark.svg"
            class="icon-checkmark" />
        </div>
        <div class="card-face is-back" style="color: black; font-size: 2rem" >
        </div>
    </div>
</template>

<style>
.card {
  position: relative;
  transition: 0.5s transform ease-in;
}
.card.is-flipped {
    transform: rotateY(180deg);
    transform-style: preserve-3d;
}
.card-face{
    width: 100%;
    height: 100%;
    position: absolute;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    backface-visibility: hidden;
}
.card-face.is-front {
    background-image: url('/images/card-bg.png');
    color: white;
    transform: rotateY(180deg);
}
.card-face.is-back {
    background-image: url('/images/card-bg-empty.png');
    color: white;
}
.icon-checkmark {
    position: absolute;
    right: 5px;
    bottom: 5px;
}
</style>