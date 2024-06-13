<template>
  <div id="app">
    <nav>
      <div class="nav-wrapper">
        <a href="#" class="brand-logo"
          ><img class="logo" src="../assets/image-removebg-preview.png" alt=""
        /></a>
        
        <ul id="nav-mobile" class="right hide-on-med-and-down">
          <li><router-link to="/formAdoption">Adote já</router-link></li>
          <li><a href="badges.html">Quem somos</a></li>
          <li><a href="/favorites">Favoritos</a></li>
        </ul>
      </div>
    </nav>

    
    <div class="flex-container">
      <img class="img-dog" src="../assets/image copy.png" alt="Imagem descritiva" />
      <div class="text-container">
        <img id="cel" src="../assets/image copy 2.png" alt="" />
        <h2 id="who">Quem somos</h2>
        <p>
          O Me Leva pra Casa é o programa de adoção responsável criado pela Vale
          que tem como objetivo encontrar novas famílias para os animais que
          foram impactados, direta ou indiretamente, pelo rompimento da barragem
          B1, em Brumadinho, e pelas evacuações e realocações preventivas em
          Minas Gerais.
        </p>
        <br />
        <p>
          Enquanto esperam pela adoção, os animais são cuidados com muito amor e
          carinho pelo nosso time de especialistas nas instalações de abrigo de
          fauna de responsabilidade da Vale.
        </p>
      </div>
    </div>

    <div class="Know">
      <div class="text-container-know">
        <h2 id="know">Conheça os bichinhos</h2>
        <p class="item2">
          <strong
            >Nossos espaços abrigam uma diversidade encantadora de animais: dos
            menores aos maiores, dos mais jovens aos mais experientes, dos mais
            tranquilos aos mais brincalhões.</strong
          >
        </p>
        <p class="item2">
          Navegue abaixo, fotos para conhecer o perfil de cada bichinho e
          escolha um para levar pra casa.
        </p>
        <p class="item2">Encontre o seu melhor amigo.</p>
      </div>
      <img class="img-know" src="../assets/image copy.png" alt="" />
    </div>

    <DogFavorites :favorites="favorites" @remove-favorite="removeFavorite" />
    <div class="dog-container">
      <DogCard
        v-for="dog in paginatedDogs"
        :key="dog.id"
        :dog="dog"
        @add-favorite="addFavorite"
      />
    </div>
    <DogPagination
      :current-page="currentPage"
      :total-pages="totalPages"
      @change-page="changePage"
    />
  </div>
</template>

<script>
import axios from "axios";
import DogCard from "../components/DogCard.vue";
import DogFavorites from "../components/DogFavorites.vue";
import DogPagination from "../components/DogPagination.vue";
import M from "materialize-css"; // Importe Materialize CSS aqui

export default {
  components: {
    DogCard,
    DogFavorites,
    DogPagination,
  },
  data() {
    return {
      dogs: [],
      favorites: JSON.parse(localStorage.getItem("favorites")) || [],
      currentPage: 1,
      itemsPerPage: 8,
    };
  },
  mounted() {
    M.AutoInit(); // Inicialize Materialize CSS no mounted hook
  },
  computed: {
    paginatedDogs() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.dogs.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.dogs.length / this.itemsPerPage);
    },
  },
  methods: {
    async fetchDogs() {
      try {
        const response = await axios.get(
          "https://dog.ceo/api/breeds/image/random/50"
        );
        this.dogs = response.data.message.map((url, index) => ({
          id: index,
          url,
        }));
      } catch (error) {
        console.error(error);
      }
    },
    addFavorite(dog) {
      if (!this.favorites.some((fav) => fav.id === dog.id)) {
        this.favorites.push(dog);
        localStorage.setItem("favorites", JSON.stringify(this.favorites));
        // Emitir evento ou redirecionar aqui se necessário
      }
    },
    removeFavorite(dogId) {
      this.favorites = this.favorites.filter((fav) => fav.id !== dogId);
      localStorage.setItem("favorites", JSON.stringify(this.favorites));
    },
    changePage(page) {
      this.currentPage = page;
    },
  },
  created() {
    this.fetchDogs();
  },
};
</script>



<style>
.nav-wrapper {
  background: #007f7b;
}

.dog-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.img-dog {
  margin-left: 50px;
}

.logo {
  width: 120px;
}

.flex-container {
  display: flex;
  align-items: flex-start;
  margin-top: 20px;
  background: #ee6f16;
  padding: 60px;
  height: 650px;
  
}



.flex-container img {
  margin-right: 20px;
}

.text-container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.text-container h2 {
  margin-bottom: 10px;
}

.text-container p {
  text-indent: 20px; /* Adjust this value for the desired indentation */
  margin-bottom: 10px;
}

p {
  margin-left: 120px;
  color: white;
  font-size: 20px;
}

#who {
  margin-left: 120px;
  color: white;
  font-size: 60px;
}

#cel {
  width: 50px;
  margin-left: 120px;
}

#know{
  margin-left: 120px;
}

.item2 {
  color: gray;
}

.flex-container {
  display: flex;
  align-items: flex-start;
  margin-bottom: 20px;
}

.flex-container img.img-dog {
  margin-right: 20px;
}

.text-container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.text-container h2 {
  margin-bottom: 10px;
}

.text-container p {
  text-indent: 20px; /* Adjust this value for the desired indentation */
  margin-bottom: 10px;
}

.Know {
  display: flex;
  align-items: flex-start;
  margin-top: 50px;
  margin: 50px;
}

.text-container-know {
  flex: 1;
  margin-left: -15px;
}

.img-know {
  margin-left: 20px;
  width: 450px;
  margin-right: 50px;
}
</style>
