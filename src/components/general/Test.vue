<template>
  <div class="carousel">
    <div class="carousel-images" :style="`transform: translateX(-${currentIndex * 100/9}%)`">
      <img v-for="(image, index) in imageList" :key="index" :src="image.src" :alt="image.alt">
    </div>
    <div class="carousel-controls">
      <button @click="previousImage">Previous</button>
      <button @click="nextImage">Next</button>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const images = [
      { src: '/src/assets/images/hero/hero-1.jpg', alt: 'Image 1' },
      { src: '/src/assets/images/hero/hero-2.webp', alt: 'Image 2' },
      { src: '/src/assets/images/hero/hero-3.webp', alt: 'Image 3' }
    ];
    const currentIndex = ref(0);

    const imageList = computed(() => {
      // Duplicate the images array to create a "virtual" carousel that loops back to the beginning and end
      return [...images, ...images, ...images];
    });

    const previousImage = () => {
      // If we're currently at the first image, cycle back to the last image of the "virtual" carousel
      if (currentIndex.value === 0) {
        currentIndex.value = imageList.value.length - images.length;
      } else {
        currentIndex.value--;
      }
    };
    
    const nextImage = () => {
      // If we're currently at the last image, cycle back to the first image of the "virtual" carousel
      if (currentIndex.value === imageList.value.length - 1) {
        currentIndex.value = images.length - 1;
      } else {
        currentIndex.value++;
      }
    };

    return {
      imageList,
      currentIndex,
      previousImage,
      nextImage
    };
  }
};
</script>

<style>
.carousel {
  position: relative;
  width: 100%;
  height: 500px;
  overflow: hidden;
}

.carousel-images {
  position: absolute;
  top: 0;
  left: 0;
  width: 300%;
  height: 100%;
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-images img {
  width: calc(100% / 3);
  height: 100%;
  object-fit: cover;
}

.carousel-controls {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  justify-content: center;
}

.carousel-controls button {
  margin: 0 10px;
  padding: 10px 20px;
  font-size: 16px;
  color: #fff;
  background-color: #333;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease-out;
}

.carousel-controls button:hover {
  background-color: #555;
}

.carousel-controls button[disabled] {
  cursor: not-allowed;
  opacity: 0.5;
}
</style>
