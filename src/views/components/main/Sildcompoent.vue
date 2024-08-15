<template>
  <div class="slider-container">
    <div class="slider" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
      <div class="slide">
        <img src="../../../../public/img/brand/mainimg.png" alt="logo" />
      </div>
      <div class="slide">
        <img src="../../../../public/img/brand/wejob.png" alt="logo" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentIndex: 0,
      slideInterval: null,
    };
  },
  mounted() {
    this.startSlider();
  },
  beforeDestroy() {
    clearInterval(this.slideInterval);
  },
  methods: {
    startSlider() {
      this.slideInterval = setInterval(() => {
        this.currentIndex = (this.currentIndex + 1) % 2;
      }, 3000); // 3초마다 이미지 전환
    },
  },
};
</script>

<style>
.slider-container {
  overflow: hidden;
  width: 50%;
  position: relative;
  margin-left: 30%;
  margin-top: 7%;
  margin-bottom: 10%;
  
}

.slider {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.slide {
  min-width: 100%;
  box-sizing: border-box;
}

.slide img {
  width: 800px;
  height: auto;
  border-radius: 5px;
}
</style>
