<template>
  <div class="modal" v-if="image" @click.self="$emit('close')">
    <div class="modal-content" ref="modal" @mousemove="handleMouseMove">
      <img :src="image.src" />
      <p>{{ image.title }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImageModal",
  props: {
    image: Object,
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content img {
  max-width: 90vw;
  max-height: 80vh;
  border-radius: 8px;
}
</style>
