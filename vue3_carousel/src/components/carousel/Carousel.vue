<template>
  <div class="carousel">
    <div class="carousel-inner">
      <CarouselIndicators
        :total="slides.length"
        :current-index="currentSlide"
        @switch="switchSlide($event)"
      ></CarouselIndicators>
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
import CarouselIndicators from "./CarouselIndicators.vue";


export default {
    props: ['slides'],
  components: { CarouselItem, CarouselControls, CarouselIndicators },
  data: () => ({
    currentSlide: 0,
    slideInterval: null,
    direction: "direction"
  }),
  methods: {
    setCurrentSlide (index) {
        this.currentSlide = index;
    },
    prev (step = -1) {
      const index = this.currentSlide > 0 ? this.currentSlide + step : this.slides.length -1;
        this.setCurrentSlide(index);
        this.direction = "left"
    },
    _next (step = 1) {
      const index = 
      this.currentSlide < this.slides.length -1 ? this.currentSlide + step : 0;
      this.setCurrentSlide(index);
      this.direction = "right"
    },
    next (step = 1) {
      this._next(step)
    },
    startSlideTimer () {
      this.stopSlideTimer();
      this.slideInterval = setInterval(() => {
        this._next();
      }, 3500)
    },
    stopSlideTimer () {
      clearInterval(this.slideInterval);
    },
    switchSlide (index) {
      const step = index - this.currentSlide
      if (step > 0) {
        this.next(step)
      }
      else {
        this.prev(step)
      }
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
