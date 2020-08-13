<template>
  <v-app dark>
    <Loading></Loading>
    <Header></Header>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <Footer></Footer>
  </v-app>
</template>

<script>
import Header from '~/components/layout/Header.vue'
import Footer from '~/components/layout/Footer.vue'
import Loading from '~/components/Loading.vue'
export default {
  components: {
    Header,
    Footer,
    Loading
  },
  data () {
    return {
    }
  }
}
</script>

<style scoped>
</style>

