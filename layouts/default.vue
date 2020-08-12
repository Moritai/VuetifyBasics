<template>
<v-app>
    <Navbar />
    <v-main>
      <Nuxt />
    </v-main>
    <Footer/>
</v-app>
</template>

<script>
import Navbar from '../components/navbar'
import Footer from '../components/footer'

export default {
	components: {
    Navbar,
    Footer
  }
   
}
</script>

<style scoped lang="scss">

</style>