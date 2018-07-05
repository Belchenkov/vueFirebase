<template>
  <nav>
    <div class="nav-wrapper  green darken-3">
      <div class="container">
        <router-link to="/" class="brand-logo">
          <span class="logo">Employee Manager</span>
        </router-link>
        <ul class="right">
          <li v-if="isLoggedIn">
            <span class="email white-text">{{ currentUser }}</span>
          </li>
          <li v-if="isLoggedIn">
            <router-link to="/">Главная</router-link>
          </li>
          <li v-if="!isLoggedIn">
            <router-link to="/login">Войти</router-link>
          </li>
          <li v-if="!isLoggedIn">
            <router-link to="/register">Регистрация</router-link>
          </li>
          <li @click="logout" v-if="isLoggedIn">
            <div class="btn blue-grey darken-2">
              Выйти
            </div>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
  import firebase from 'firebase';

  export default {
    name: 'navbar',
    data () {
      return {
        isLoggedIn: false,
        currentUser: false
      }
    },
    created() {
      if (firebase.auth().currentUser) {
        this.isLoggedIn = true;
        this.currentUser = firebase.auth().currentUser.email;
      }
    },
    methods: {
      logout () {
        firebase
        .auth()
        .signOut()
          .then(() => {
            this.$router.go({ path: this.$router.path });
          })
      }
    }  
  }
</script>


<style>
  @import url('https://fonts.googleapis.com/css?family=Galada');

  .brand-logo {
    font-family: 'Galada', cursive;
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
  }

  ul.right {
      box-shadow: none;
    }

  ul.right li {
    box-shadow: none;
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);

  }
  
</style>
