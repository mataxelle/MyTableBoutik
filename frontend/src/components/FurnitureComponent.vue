<template>
    <div>
        <h1>page</h1>
        <p>je suis sur la page</p>
        <h3>{{ furniture.name }}</h3>
        <img v-bind:src="furniture.imageUrl" alt="image d'un meuble">
        <p>Prix : {{ furniture.price / 100 }}€</p>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "FurnitureComponent",

    data() {
        return {
            furniture: {}
        }
    },

    mounted() {
        axios.get("http://localhost:3000/api/furniture/" + this.$route.params.furnitureId)
        .then((response) => {
            this.furniture = response.data;
        })
        .catch((e) => {
            console.log(e);
        });
    }
    
}
</script>