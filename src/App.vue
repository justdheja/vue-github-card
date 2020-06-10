<template>
  <div id="app" class="hero is-fullheight">

    <search-user/>

    <user-card/>

    <footer>
      Made with 💛 by justdheja
    </footer>
  </div>
</template>

<script>
import UserCard from './components/UserCard.vue'
import SearchUser from './components/SearchUser.vue'

export default {
  name: 'App',
  components: {
    UserCard,
    SearchUser
  }
}
</script>

<style lang="scss">
@import url("./assets/main.scss");
</style>
