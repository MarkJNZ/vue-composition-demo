<template>
  <div id="app">
    <div class="form">
      <label for="username">{{dictionary.usernameLabel}}:</label>
      <input id="username" class="input" :value="username" @input="updateUsername" />
      <label for="password">{{dictionary.passwordLabel}}:</label>
      <input id="password" type="password" class="input"
      :value="password" @input="updatePassword" />
      <button class="submit" @click="submit">{{dictionary.signupLabel}}</button>
    </div>
    <div class="language-container">
      <label for="language">{{dictionary.languageLabel}}:  </label>
      <input type="radio" name="language" value="en" v-model="language"/>English
      <input type="radio" name= "language" value="es" v-model="language"/>Español
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import en from './constants/en.json';
import es from './constants/es.json';

export default {
  name: 'app',
  data() {
    return {
      username: '',
      password: '',
      language: 'en',
    };
  },
  methods: {
    updateUsername(event) {
      this.username = event.target.value;
    },
    updatePassword(event) {
      this.password = event.target.value;
    },
    async submit() {
      // probably add some other business logic here :)
      await axios.post('https://jsonplaceholder.typicode.com/users', {
        username: this.username,
        password: this.password,
      });
      alert('User created');
    },
  },
  computed: {
    dictionary() {
      return this.language === 'es' ? es : en;
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.input {
  padding: 10px;
  font-size: 12px;
  outline: none;
  margin: 10px 0;
}

.form {
  display: flex;
  flex-direction: column;
  width: 30vw;
  margin: auto;
}

.submit {
  padding: 10px;
  border: none;
  background: #00aced;
  color: #fff;
  font-size: 15px;
  cursor: pointer;
}

.language-container {
  width: 50vw;
  margin: auto;
  padding-top: 40px;
}

label {
  text-align: left;
}
</style>
