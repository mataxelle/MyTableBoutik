<template>
    <div class="furniture_page">
        <h1>{{ furniture.name }}</h1>
        <img v-bind:src="furniture.imageUrl" alt="image d'un meuble">
        <p>Prix : {{ furniture.price / 100 }}€</p>
        <form action="">
            <label for="varnish">Choisissez votre vernis :</label>
            <select v-model="selected" name="varnish" id="varnish">
                <option v-for="varnishsOption in varnishsOptions" :key="varnishsOption" :value="varnishsOption">{{ varnishsOption }}</option>
            </select>
        </form>
        <p>Description :</p>
        <p>{{ furniture.description }}</p>
        <button @click="sendItemToCart">Ajouter au panier</button>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "FurnitureComponent",

    data() {
        return {
            furniture: {},
            varnishsOptions: [],
            selected: '',
        }
    },

    mounted() {
        axios.get("http://localhost:3000/api/furniture/" + this.$route.params.furnitureId)
        .then((response) => {
            this.furniture = response.data;
            this.varnishsOptions = response.data.varnish;
            this.options = response.data.varnish;
        })
        .catch((e) => {
            console.log(e);
        });

        /*if (!localStorage.getItem('cartItem')) {
            localStorage.setItem('cartItem', JSON.stringify([]))}*/
    },

    methods: {
        sendItemToCart() {

            let cartLocalStorage = JSON.parse(localStorage.getItem('cartItem'));

            const choisedItem = {
                id: this.furniture._id,
                name: this.furniture.name,
                varnish: this.selected,
                price: this.furniture.price,
                quantity: 1
            };

            const itemToCartOk = () => {
                if (this.selected) {
                    cartLocalStorage.push(choisedItem);
                } else {
                    alert('Choisissez un vernis s\' vous plaît !');
                }
            };

            if (!cartLocalStorage) {

                cartLocalStorage = [];
                itemToCartOk();

            } else {

                itemToCartOk();
            }

            localStorage.setItem('cartItem', JSON.stringify(cartLocalStorage));
            this.$router.replace({
                path: "/cart"
            });
        }
    }
    
}
</script>

<style scoped>
.furniture_page {
    display: flex;
    align-items: center;
    flex-direction: column;
}
img {
    max-width: 80%;
    height: auto;
}
</style>