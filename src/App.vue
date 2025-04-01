<script setup lang="ts"></script>

<template>
  <div class="app">
    <h1>이미지 갤러리</h1>
    <div class="gallery">
      <ImageCard
        v-for="img in filteredImages"
        :key="img.id"
        :image="img"
        @select="selectedImage = $event"
      />
    </div>

    <ImageModal :image="selectedImage" @close="selectedImage = null" />
  </div>
</template>

<script>
import ImageCard from "./components/ImageCard.vue";
import ImageModal from "./components/ImageModal.vue";

export default {
  components: {
    ImageCard,
    ImageModal,
  },
  data() {
    return {
      images: [
        {
          id: 1,
          src: "https://images.unsplash.com/photo-1741936428950-3f66f0a69320?q=80&w=1127&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          title: "galaxy",
        },
        {
          id: 2,
          src: "https://images.unsplash.com/photo-1741936428950-3f66f0a69320?q=80&w=1127&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          title: "galaxy",
        },
      ],
      selectedImage: null,
    };
  },
  computed: {
    filteredImages() {
      return this.images;
    },
  },
};
</script>

<style>
.app {
  text-align: center;
  padding: 1.25rem;
}
.gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
