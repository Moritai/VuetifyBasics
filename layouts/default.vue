<template>
<v-app>
    <Navbar />
    <div class="pages">
      <Nuxt />
    </div>
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
  .pages{
    margin-top: 4em;
  }
</style>