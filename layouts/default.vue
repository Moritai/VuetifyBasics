<template>
<v-app>
    <Navbar />
    <div class="pages">
      <Nuxt />
    </div>
</v-app>
</template>

<script>
import Navbar from '../components/navbar'
export default {
	components: {
		Navbar
  }
   
}
</script>

<style scoped lang="scss">
  .pages{
    margin-top: 4em;
  }
</style>