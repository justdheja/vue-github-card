<template>
  <div id="app" class="hero is-fullheight">

    <form class="form">
      <input v-on:keyup.enter="console.log(username)" v-model="username" class="form__field" placeholder="Github Username"/>
      <button @click="getUser" type="button" class="btn btn--primary btn--inside uppercase">Search</button>
    </form>

    <user-card :user="github"/>

    <footer>
      Made with 💛 by justdheja
    </footer>
  </div>
</template>

<script>
import UserCard from './components/UserCard.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    UserCard,
  },
  data() {
    return {
      github: null,
      username: null
    }
  },
  created() {
    
  },
  methods: {
    getUser(){
      console.log(this.username)
      axios.get(`https://api.github.com/users/${this.username}`)
      .then(Response => {
        console.log(Response)
        this.github = Response
      })
      this.username = ''
    }
  },

}
</script>

<style lang="scss">
@import url("./assets/main.scss");

$background: #f5f6fa;
$text: #000000;
$input-bg-color: #fff;
$input-text-color: #a3a3a3;
$button-bg-color: #2c2d30;
$button-bg-color-mobile: #094256;
$button-text-color: #fff;

// button
.btn {
  border-radius: 50%;
	display: inline-block;
	background: transparent;
	color: inherit;
	font: inherit;
	border: 0;
	outline: 0;
	padding: 0;
	transition: all 200ms ease-in;
	cursor: pointer;
	
	&--primary {
		background: $button-bg-color;
    color: $button-text-color;
    font-size: 10px;
		box-shadow: 0 0 10px 2px rgba(0, 0, 0, .1);
		border-radius: 5px;
		padding: 10px 30px;
		
		&:hover {
      background: darken($button-bg-color, 10%);
      margin-left: -40px;
		}
		
		&:active {
			background: $button-bg-color;
			box-shadow: inset 0 0 10px 2px rgba(0, 0, 0, .2);
		}
	}
	
	&--inside {
		margin-left: -50px;
	}
}

// form
.form {	
  &__field {
  height: 10px;
		width: 350px;
		background: #fff;
		color: $input-text-color;
		font: inherit;
		box-shadow: 0 6px 10px 0 rgba(0, 0, 0 , .1);
    border: 0;
    border-radius: 5px;
		outline: 0;
		padding: 22px 18px;
	}
}

// mobile

@media screen and (max-width: 1025px) {
  .form{
    &__field{
      width: 250px;
    }
  }
  .btn{
    &--primary{
      background: $button-bg-color-mobile;
    }
  }
}
</style>
