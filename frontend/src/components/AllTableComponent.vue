<template>
  <div>
    <h1>My Table Boutik</h1>

    <p>Depuis 1986, nous vendons des meubles vintage.</p>

    <h2>Faites de belles affaires ! </h2>

    <div v-if="furnitures && furnitures.length">
      <div v-for="furniture of furnitures" :key="furniture.id" :furniture="furniture" class="furniture_box">
        <h3>{{ furniture.name }}</h3>
        <img v-bind:src="furniture.imageUrl" alt="image d'un meuble">
        <p>Prix : {{ furniture.price / 100 }}€</p>
        <router-link :to="{ name: 'Furniture', params: { furnitureId: furniture._id }}">Voir le produit</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AllTable",

  data() {
    return {
      furnitures: [],
    };
  },

  created() {
    axios
      .get("http://localhost:3000/api/furniture")
      .then((response) => {
        this.furnitures = response.data;
      })
      .catch((e) => {
        console.log(e);
      });
  },
};
</script>

<style scoped>
.furniture_box {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 40px 0;
}
img {
  width: 350px;
  height: 300;
}
</style>