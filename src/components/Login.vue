<template>
  <div>
    <div class="container">
    <div class="row">
      <div class="col s12 m8 offset-m2">
        <div class="login card-panel blue-grey darken-2 white-text center z-depth-3">
          <h3>Войти</h3>
          <form action="index.html">
            <div class="input-field">
              <input type="email" id="email" v-model="email">
              <label class="white-text" for="email">
                <i class="far fa-envelope left"></i>
                Email
                </label>
            </div>
            <div class="input-field">
              <input type="password" id="password" v-model="password">
              <label class="white-text" for="password">
                <i class="fas fa-lock left"></i>Пароль
              </label>
            </div>
            <button
              @click.prevent="login" 
              class="btn btn-large z-depth-3 btn-extended blue lighten-1 white-text"
             >Войти</button>
          </form>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import firebase from 'firebase';
export default {
  name: 'login',
  data () {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    login () {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            M.toast({html: `Вы вошли по именем ${user.email}`});
            this.$router.go({ path: this.$router.path });
          },
          err => {
            alert(err.message);
          }
        );
    }
  }
};
</script>

<style>
  .login {
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
  }
</style>
