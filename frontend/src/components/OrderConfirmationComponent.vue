<template>
    <div>
        <h1>Confirmation commande page</h1>

        <p>Numéro de commande : {{ order.orderId }}</p>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "OrderConfirmationComponent",

    data: () => {
        return {
            order: {}
        }
    },

    mounted() {
        axios.get("http://localhost:3000/api/order-confirmation/" + this.$route.params.orderId)
        .then((response) => {
            this.order = response.data;
        })
        .catch((e) => {
            console.log(e);
        });
    }
}
</script>