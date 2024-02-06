<template>
<transition name="slide-in">
  <div class="carousel-item" v-show="currentSlide === index">
    <img :src="slide" >
  </div>
</transition>

</template>


<script>
export default {
    props: ["slide", "currentSlide", "index"],
}
</script>

<style>
.carousel-item {
  position: absolute; 
  inset: 0;
}

.slide-in-enter-active,
.slide-in-leave-active {
  transition: all 1s ease-in-out;
}

.slide-in-enter-from {
  transform: translateX(-100%)
}

.slide-in-leave-to {
  transform: translateX(100%)
}

img { 
  height: 400px;
  width: 900px;
}
</style>