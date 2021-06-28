<template>
  <div class="home">
    <OrderConfirmationComponent/>
  </div>
</template>

<script>
import OrderConfirmationComponent from '@/components/OrderConfirmationComponent.vue'

export default {
  name: 'OrderConfirmation',
  components: {
    OrderConfirmationComponent
  }
}
</script>