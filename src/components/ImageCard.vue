<template>
  <div class="image-card">
    <img :src="image.src" :alt="image.title" @click="$emit('select', image)" />
    <p>{{ image.title }}</p>
  </div>
</template>

<script>
export default {
  name: "ImageCard",
  props: {
    image: Object,
  },
};
</script>

<style scoped>
.image-card {
  cursor: pointer;
  width: 200px;
  margin: 10px;
}
.image-card img {
  width: 100%;
  height: auto;
  border-radius: 8px;
}
</style>
