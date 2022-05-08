<template>
  <HSMenu />
  <router-view />
  <HSFooter />
  <Snackbar />
</template>
<script>
import HSMenu from './components/header/main_header_2.vue'
import HSFooter from './components/footer/footer.vue'
import Snackbar from './components/partial/snackbar.vue'

export default {
  components: {
    HSMenu,
    HSFooter,
    Snackbar,
  },

}

</script>
