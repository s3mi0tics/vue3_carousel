<template>
  <div class="carousel">
    <div class="carousel-inner">
      <carouselItem
        v-for="(slide, index) in slides"
        :slide="slide"
        :key="`item-${index}`"
        :current-slide="currentSlide"
        :index="index"
        :direction="direction"
        @mouseenter="stopSlideTimer"
        @mouseout="startSlideTimer"
      ></carouselItem>
      <CarouselControls 
        @prev="prev" 
        @next="next"
        @mouseenter="stopSlideTimer"
        @mouseout="startSlideTimer"
      ></CarouselControls>
    </div>
  </div>
</template>

<script>
import CarouselItem from "./CarouselItem.vue";
import CarouselControls from "./CarouselControls.vue";
import { toHandlers } from "vue";
export default {
    props: ['slides'],
  components: { CarouselItem, CarouselControls },
  data: () => ({
    currentSlide: 0,
    slideInterval: null,
    direction: "direction"
  }),
  methods: {
    setCurrentSlide (index) {
        this.currentSlide = index;
    },
    prev () {
      const index = this.currentSlide > 0 ? this.currentSlide - 1 : this.slides.length -1;
        this.setCurrentSlide(index);
        this.direction = "left"
    },
    _next () {
      const index = 
      this.currentSlide < this.slides.length -1 ? this.currentSlide + 1 : 0;
      this.setCurrentSlide(index);
      this.direction = "right"
    },
    next () {
      this._next()
    },
    startSlideTimer () {
      this.stopSlideTimer();
      this.slideInterval = setInterval(() => {
        this._next();
      }, 3500)
    },
    stopSlideTimer () {
      clearInterval(this.slideInterval);
    }
  },
  mounted () {
    this.startSlideTimer()
  },
  beforeUnmount () {
    this.stopSlideTimer()
  }
};
</script>

<style scoped>
.carousel{
    display: flex;
    justify-content: center;
}

.carousel-inner {
    position: relative;
    width: 900px;
    height: 400px;
    overflow: hidden;
}
</style>
