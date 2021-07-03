<template>
  <div class="home">
    <CartComponent/>
    <div v-if="itemInLocal === true">
      <UserInformationComponent/>
    </div>
  </div>
</template>

<script>
import CartComponent from '@/components/CartComponent.vue'
import UserInformationComponent from "@/components/UserInformationComponent.vue"

export default {
  name: 'Cart',
  components: {
    CartComponent,
    UserInformationComponent
  },

  data() {
    return {
      itemInLocal: []
    }
  },

  mounted() {

    const cartLocalStorage = JSON.parse(localStorage.getItem("cartItem"));

    this.itemInLocal = cartLocalStorage.length > 0;
  }
}
</script>