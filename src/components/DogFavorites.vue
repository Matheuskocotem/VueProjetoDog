<!-- src/components/DogFavorites.vue -->
<template>
  <div class="favorites">
    <h2>Favorites</h2>
    <div v-if="favorites.length">
      <div v-for="dog in favorites" :key="dog.id" class="favorite-item">
        <img :src="dog.url" alt="dog image" />
        <button @click="$emit('remove-favorite', dog.id)">Remove</button>
      </div>
    </div>
    <p v-else>No favorites added.</p>
  </div>
</template>

<script>
export default {
  props: ['favorites']
};
</script>

<style>
.favorites {
  margin-bottom: 20px;
}
.favorite-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.favorite-item img {
  width: 50px;
  height: 50px;
  margin-right: 10px;
}
</style>
