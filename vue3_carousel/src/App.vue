<template>
  <carousel :slides="slides"></carousel>
</template>

<script>

import Carousel from "./components/carousel/Carousel.vue";
export default {
  name: 'App',
  components: { Carousel },
  data: () => ({
    slides: [ 
      require("@/assets/home.png"),
      require('@/assets/new_job.png'),
      require('@/assets/job_details.png'),
      require('@/assets/schedule_job.png')
    ]
  })
}


</script>

<style>

</style>
