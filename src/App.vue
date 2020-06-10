<template>
  <div id="app" class="hero is-fullheight">

    

    <user-card/>

    <footer>
      Made with 💌 by justdheja
    </footer>
  </div>
</template>

<script>
import UserCard from './components/UserCard.vue'

export default {
  name: 'App',
  components: {
    UserCard
  }
}
</script>

<style lang="scss">
@import url("./assets/main.scss");
</style>
