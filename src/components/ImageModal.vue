<template>
  <div class="modal" v-if="image" @click.self="$emit('close')">
    <div
      class="modal-content"
      ref="modal"
      @mousemove="handleMouseMove"
      @mouseleave="resetLight"
    >
      <img :src="image.src" />
      <div class="dark-overlay" :style="lightMaskStyle"></div>

      <p class="title">{{ image.title }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
const props = defineProps({
  image: Object,
});
const emit = defineEmits(["close"]);

const modal = ref(null);
const lightX = ref(0);
const lightY = ref(0);

const showLight = ref(false);

const handleMouseMove = (e) => {
  const rect = modal.value.getBoundingClientRect();
  const x = e.clientX - rect.left;
  const y = e.clientY - rect.top;
  lightX.value = x;
  lightY.value = y;

  lightMaskStyle.value = {
    "--x": `${x}px`,
    "--y": `${y}px`,
  };
};

const lightMaskStyle = ref({});
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

.modal-content {
  position: relative;
  max-width: 90vw;
  max-height: 80vh;
  border-radius: 8px;
  overflow: hidden;
}

.modal-content img {
  width: 100%;
  display: block;
}

.title {
  font-size: 5rem;
}

.dark-overlay {
  position: absolute;
  inset: 0;
  background: #000000; /* 전체 어둡게 */
  pointer-events: none;
  z-index: 10;

  /* 조명처럼 비추기 위해 마스크 사용 */
  -webkit-mask-image: radial-gradient(
    circle 200px at var(--x, 50%) var(--y, 50%),
    transparent 0%,
    black 100%
  );
  mask-image: radial-gradient(
    circle 200px at var(--x, 50%) var(--y, 50%),
    transparent 0%,
    black 100%
  );
  mask-composite: exclude;
  -webkit-mask-composite: destination-out;
}
</style>
