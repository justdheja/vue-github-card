<template>
  <div id="app" class="hero is-fullheight">

    <search-user :username="userinput" :propsfunction="getUser"/>

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
      github: null,
      userinput: null
    }
  },
  created() {
    axios.get("https://api.github.com/users/justdheja")
      .then(Response => {
        console.log(Response)
        this.github = Response
      })
  },
  methods: {
    getUser(){
      console.log(this.userinput)
    }
  },

}
</script>

<style lang="scss">
@import url("./assets/main.scss");
</style>
