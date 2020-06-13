<template>
<div>
  <div v-if="userExist" class="outer-div">
  <div class="inner-div">
    <div class="front">
      <img :src="bgCard" alt="" class="front__bkg-photo">
      <img :src="user.data.avatar_url" alt="" class="front__face-photo">
      <div class="front__text">
        <h3 class="front__text-header">{{user.data.name}}</h3>
        <h3 class="front__text-subheader">{{user.data.login}}</h3>
        <p v-if="user.data.location" class="front__text-para"><i class="fas fa-map-marker-alt front-icons"></i>{{user.data.location}}</p>
        <p class="front__text-info">
          {{user.data.followers}} Followers - {{user.data.following}} Following
          <br>
          {{user.data.public_repos}} {{user.data.public_repos > 1 ? 'Repos' : 'Repo'}}
          <br>
        </p>


        
        <span class="front__text-hover">View More</span>
      </div>
    </div>
    <div class="back">
      <span v-if="user.data.bio" class="front__text-bio">
        <strong>
          Bio:
          <br>
        </strong>
        {{user.data.bio}}
        <hr>
      </span>
      <br>
      <div class="social-media-wrapper">
        <a :href="user.data.html_url" target="_blank" class="social-icon"><i class="fab fa-github-square" aria-hidden="true"></i></a>
        <a v-if="user.data.blog" :href="`https://${user.data.blog}`" target="_blank" class="social-icon"><i class="fas fa-link" aria-hidden="true"></i></a>
      </div>
    </div>

    </div>
  </div>
  <div>
    <h1 class="not-found">User Not Found</h1>
  </div>
</div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      required: false
    }
  },
  computed: {
    userExist(){
      if(this.user.status === 200){
        return true
      } else {
        return false
      }
    },
    bgCard(){
      var repos = this.user.data.public_repos
      if(repos > 15){
        return "https://images.unsplash.com/photo-1519389950473-47ba0277781c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80"
      } else if (repos < 5) {
        return "https://images.unsplash.com/photo-1516653980844-c68df1de5249?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80"
      } else {
        return "https://images.unsplash.com/photo-1558710763-9791081edd44?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1951&q=80"
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$black: #071011;
$white: #fff;
$red: #ff434c;
$standard: 10px;
$card-height: 400px;
$card-width: 250px;

.not-found{
  color: $white;
  font-weight: 700;
}


.outer-div,
.inner-div {
  height: $card-height;
  max-width: $card-width;
  margin: 0 auto;
  position: relative;
}

.outer-div {
  perspective: 900px;
  perspective-origin: 50% calc(50% - 18em);
}

.inner-div {
  margin: $standard * 0 auto;

  border-radius: 5px;
  font-weight: 400;
  color: $black;
  font-size: 1rem;
  text-align: center;
  transition: all 0.6s cubic-bezier(0.8, -0.4, 0.2, 1.7);
  transform-style: preserve-3d;

  &:hover {
    transform: rotateY(-180deg);
    background-color: transparent;
  }

  &:hover .social-icon {
    opacity: 1;
    top: 0;
  }

  &:hover .front__face-photo,
  &:hover .front__footer {
    opacity: 0;
  }
}

.front,
.back {
  position: relative;
  top: 0;
  left: 0;
  backface-visibility: hidden;
}

.front {
  cursor: pointer;
  height: 100%;
  background: $white;
  backface-visibility: hidden;
  border-radius: 5px;
  box-shadow: 0 15px 10px -10px rgba(0, 0, 0, 0.5), 0 1px 4px rgba(0, 0, 0, 0.3),
    0 0 40px rgba(0, 0, 0, 0.1) inset;
}

.front__bkg-photo {
  position: relative;
  height: 110px;
  width: $card-width;
  backface-visibility: hidden;
  overflow: hidden;
  border-top-right-radius: 5px;
  border-top-left-radius: 5px;

  &:after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
  }
}

.front__face-photo {
  position: relative;
  top: -60px;
  height: 110px;
  width: 110px;
  margin: 0 auto;
  border-radius: 50%;
  border: 5px solid $white;
  background-size: contain;
  backface-visibility: hidden;
  overflow: hidden;
  transition: all 0.6s cubic-bezier(0.8, -0.4, 0.2, 1.7);
  z-index: 3;
}

.front__text {
  position: relative;
  top: -55px;
  margin: 0 auto;
  font-family: "Montserrat";
  font-size: 18px;
  backface-visibility: hidden;

  .front__text-header {
    font-weight: 700;
    text-decoration: underline;
  }

  .front__text-subheader {
    font-weight: 400;
    font-size: 14px;
  }

  .front__text-para {
    position: relative;
    top: -5px;
    margin-top: 5px;
    color: #000;
    font-size: 10px;
    letter-spacing: 0.4px;
    font-weight: 400;
    font-family: "Montserrat", sans-serif;
  }

  .front__text-info {
    font-size: 10px;
  }


  .front-icons {
    position: relative;
    top: 0;
    font-size: 10px;
    margin-right: 6px;
    color: gray;
  }

  .front__text-hover {
    position: relative;
    top: 10px;
    font-size: 10px;
    color: $red;
    backface-visibility: hidden;

    font-weight: 700;
    text-transform: uppercase;

    border: 2px solid $red;
    padding: 8px 15px;
    border-radius: 30px;

    background: $red;
    color: $white;
    box-shadow: 0 11px 20px -12px rgba(0, 0, 0, 0.6);
  }
}

.back {
  transform: rotateY(180deg);
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: $black;
  border-radius: 5px;
  display: block;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  color: #fff;
  padding: 25px;
  hr{
    border: 1px solid white;
  }
}

.social-media-wrapper {
  font-size: 36px;

  .social-icon {
    position: relative;
    top: 20px;
    margin-left: 5px;
    margin-right: 5px;
    opacity: 0;
    color: #fff;
    transition: all 0.4s cubic-bezier(0.3, 0.7, 0.1, 1.9);
  }

  .social-icon:nth-child(1) {
    transition-delay: 0.6s;
  }

  .social-icon:nth-child(2) {
    transition-delay: 0.7s;
  }

  .social-icon:nth-child(3) {
    transition-delay: 0.8s;
  }

  .social-icon:nth-child(4) {
    transition-delay: 0.9s;
  }
}

.fab {
  position: relative;
  top: 0;
  left: 0;
  transition: all 200ms ease-in-out;
}

.fab:hover {
  top: -7px;
}

.fas {
  position: relative;
  top: 0;
  left: 0;
  transition: all 200ms ease-in-out;
}

.fas:hover {
  top: -7px;
}

</style>
