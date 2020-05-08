/* eslint-disable no-alert */

<template>
  <div class="Vue3Signup">
    <div class="form">
      <label for="username">{{ dictionary.usernameLabel }}:</label>
      <input
        id="username"
        class="input"
        :value="username"
        @input="updateUsername"
      />
      <label for="password">{{ dictionary.passwordLabel }}:</label>
      <input
        id="password"
        type="password"
        class="input"
        :value="password"
        @input="updatePassword"
      />
      <button class="submit" @click="submit">
        {{ dictionary.signupLabel }}
      </button>
    </div>
    <div class="language-container">
      <label for="language">{{ dictionary.languageLabel }}: </label>
      <input
        type="radio"
        name="language"
        value="en"
        v-model="language"
      />English
      <input
        type="radio"
        name="language"
        value="es"
        v-model="language"
      />Español
    </div>
  </div>
</template>

<script>
  import axios from "axios";
  import { ref, computed } from "@vue/composition-api";
  import en from "../constants/en.json";
  import es from "../constants/es.json";

  const useLogin = () => {
    const username = ref("");
    const password = ref("");
    const updateUsername = event => {
      username.value = event.target.value;
    };
    const updatePassword = event => {
      password.value = event.target.value;
    };
    const submit = async () => {
      // probably add some other business logic here :)
      await axios.post("https://jsonplaceholder.typicode.com/users", {
        username,
        password
      });
      alert("User created");
    };
    return {
      username,
      password,
      updateUsername,
      updatePassword,
      submit
    };
  };

  const useLanguage = () => {
    const language = ref("en");
    const dictionary = computed(() => (language.value === "es" ? es : en));
    return {
      language,
      dictionary
    };
  };

  export default {
    name: "Vue3Signup",
    setup() {
      return {
        ...useLogin(),
        ...useLanguage()
      };
    }
  };
</script>

<style>
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
