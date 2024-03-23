<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <div class="carouselContainer">

    <div class="buttonContainer">
      <button class="leftButton" @click="prevSlide" :style="{ visibility: activeSlide === 0 ? 'hidden' : 'visible' }">
        <svg class="buttonSVG" width="24" height="24" viewBox="0 0 24 24">
          <polygon points="15.293 3.293 6.586 12 15.293 20.707 16.707 19.293 9.414 12 16.707 4.707 15.293 3.293"/>
        </svg>
      </button>
      <button class="rightButton" @click="nextSlide" :style="{ visibility: activeSlide === numberOfSlidesArray.length - 1 ? 'hidden' : 'visible' }">
        <svg class="buttonSVG" width="24" height="24" viewBox="0 0 24 24">
          <polygon points="7.293 4.707 14.586 12 7.293 19.293 8.707 20.707 17.414 12 8.707 3.293 7.293 4.707"/>
        </svg>
      </button>
    </div>

    <div class="dotContainer">
      <button v-for="(dot, index) in numberOfSlidesArray" :key="index" class="dot" :class="{ active: index === activeSlide }" @click="goToSlide(index)">○</button>
    </div>
    
    <div class="carousel" ref="carousel" @scroll="handleScroll">
      <img src="../../public/assets/1.jpg"/>
      <img src="../../public/assets/2.jpg"/>
      <img src="../../public/assets/3.jpg"/>
      <img src="../../public/assets/4.jpg"/>
      <img src="../../public/assets/5.jpg"/>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeSlide: 0,
      numberOfSlidesArray: []
    };
  },

  methods: {
    nextSlide() {
      this.$refs.carousel.scrollLeft += this.$refs.carousel.offsetWidth;
    },

    prevSlide() {
      this.$refs.carousel.scrollLeft -= this.$refs.carousel.offsetWidth;
    },

    handleScroll() {
      this.activeSlide = Math.round(this.$refs.carousel.scrollLeft / this.$refs.carousel.offsetWidth);
    },

    goToSlide(index) {
      this.$refs.carousel.scrollLeft = index * this.$refs.carousel.offsetWidth;
    }

  },
  
  mounted() {
    for (let i = 0; i < this.$refs.carousel.childElementCount; i++) {
      this.numberOfSlidesArray.push(i); 
    }
}
};
</script>


