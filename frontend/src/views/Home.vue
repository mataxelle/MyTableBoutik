<template>
  <div class="home">
    <AllTableComponent/>
    <FooterComponent/>
  </div>
</template>

<script>
// @ is an alias to /src
import AllTableComponent from '@/components/AllTableComponent.vue'
import FooterComponent from '@/components/FooterComponent.vue'

export default {
  name: 'Home',
  components: {
    AllTableComponent,
    FooterComponent
  }
}
</script>
