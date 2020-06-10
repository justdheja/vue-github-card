<template>
  <div id="app" class="hero is-fullheight">

    <search-user/>

    <user-card :user="github"/>

    <footer>
      Made with 💛 by justdheja
    </footer>
  </div>
</template>

<script>
import UserCard from './components/UserCard.vue'
import SearchUser from './components/SearchUser.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    UserCard,
    SearchUser
  },
  data() {
    return {
      github: null
    }
  },
  created() {
      axios.get("https://api.github.com/users/victoriatrinita")
        .then(Response => {
          console.log(Response)
          this.github = Response
        })
  },

}
</script>

<style lang="scss">
@import url("./assets/main.scss");
</style>
