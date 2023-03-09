<template>
  <section id="hero">
    <img :src="props.items[currentItem].src" :alt="props.items[currentItem].name">
    <div class="wrap">
      <h1>Building things <br> is our mission.</h1>
      <div class="hero-info">
        <div class="hero-info-description">
          <p>Feature projects</p>
          <p>{{ props.items[currentItem].name }}</p>
        </div>
        <div class="hero-info-buttons">
          <button @click=changeCurrentItem(-1)>
            <img src="../../assets/images/icons/arrow-left.png" alt="">
            Back</button>
          <button @click=changeCurrentItem(1)>
            Next
            <img src="../../assets/images/icons/arrow-right.png" alt="">
          </button>
        </div>
      </div>
    </div>
  </section>
</template>
<script setup lang="ts">
import { ref } from "vue"
interface Item {
  name: string;
  src: string;
}
const props = defineProps<{
  items: Item[]
}>()
const currentItem = ref(0)
function changeCurrentItem(dir: 1 | -1) {
  if (dir === 1) {
    if (currentItem.value < props.items.length - 1) {
      currentItem.value++
    } else {
      currentItem.value = 0
    }
  } else {
    if (currentItem.value > 0) {
      currentItem.value--
    } else {
      currentItem.value = props.items.length - 1
    }
  }
}
</script>
<style lang="postcss">
#hero {
  height: 700px;
  position: relative;
  display: flex;
  align-items: center;

  .wrap {
    margin: 0;
  }

  >img {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }

  h1 {
    font-weight: 600;
    font-size: 72px;
    line-height: 84px;
    color: #292E3D;
  }

  .hero-info {
    position: absolute;
    right: 0;
    bottom: 0;
    background-color: #3559C7;
    color: #fff;
    min-width: 410px;

    &-description {
      padding: 20px 50px;
      text-align: center;
      max-width: 310px;

      p:first-of-type {
        font-weight: 700;
        margin-bottom: 20px;
      }

      p:last-of-type {
        font-size: 24px;
      }
    }

    &-buttons {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      background-color: #fff;
      gap: 1px;
    }

    button {
      display: flex;
      align-items: center;
      justify-content: center;
      background: #292E3D;
      color: #fff;
      border: none;
      gap: 10px;
      padding: 10px 0;
    }
  }
}
</style>