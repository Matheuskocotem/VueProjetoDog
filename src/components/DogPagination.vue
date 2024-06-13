<!-- src/components/DogPagination.vue -->
<template>
  <div class="pagination">
    <button
      v-for="page in totalPages"
      :key="page"
      :class="{ active: page === currentPage }"
      @click="$emit('change-page', page)"
    >
      {{ page }}
    </button>
  </div>
</template>

<script>
export default {
  props: ['currentPage', 'totalPages']
};
</script>

<style>
.pagination {
  margin-top: 20px;
  height: 50px;
  padding: 2px;
  text-align: center;
  }
  .pagination button {
    margin: 0 5px;
    padding: 5px 10px;
    background-color: #FFC107;
    border-radius: 100%;
    border: none;
    color: white;
}
.pagination .active {
  font-weight: bold;
}

.pagination button:hover{
  background-color:#c7961c;
  cursor: pointer;
  transform: scale(1.05);
}
</style>
