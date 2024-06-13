<template>
    <div>
        <h1>Seus Favoritos</h1>
        <ul>
            <li v-for="favorite in favorites" :key="favorite.id">
                <img :src="favorite.url" alt="Dog" />
                
            </li>
            <li><router-link to="/formAdoption">Adote já</router-link></li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'SeuFavorito',
    data() {
        return {
            favorites: JSON.parse(localStorage.getItem('favorites')) || [],
        };
    },
};
</script>

<style scoped>
ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 10px;
}

img {
    width: 200px;
    height: auto;
    border-radius: 10px;
}
</style>
