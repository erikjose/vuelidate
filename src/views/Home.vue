<template>
  <div class="home">
    <pre>
      {{ $v.$invalid }}
    </pre>
    <form action>
      <label for="name">Nome:</label>
      <input v-model="name" type="text" @change="$v.name.$touch()" name="name" id="name" />
      <p v-if="$v.name.$error">Este campo é requerido.</p>

      <label for="email">Email:</label>
      <input type="text" v-model="email" name="email" @change="$v.email.$touch()" />
      <p v-if="$v.email.$error">Este e-mail é inválido.</p>

      <label for="password">Defina sua senha:</label>
      <input
        v-model="password"
        @change="$v.password.$touch()"
        type="password"
        name="password"
        id="password"
      />
      <p v-if="$v.password.$error">Este campo é requerido.</p>

      <label for="confirmation_pass">Confirme sua senha:</label>
      <input
        v-model="confirmation_password"
        @change="$v.confirmation_password.$touch()"
        type="password"
        name="c-password"
        id="c-password"
      />
      <p v-if="$v.confirmation_password.$error">As senhas não coincidem.</p>

      <button type="submit" @click.prevent="login()">Fazer login</button>
    </form>

    <router-link to="/curso">Cadastrar curso</router-link>
  </div>
</template>

<script>
import { required, email, sameAs } from "vuelidate/lib/validators";

export default {
  name: "home",
  data: () => ({
    name: "",
    email: "",
    password: "",
    confirmation_password: ""
  }),
  validations: {
    name: { required },
    email: { required, email },
    password: { required },
    confirmation_password: {
      required,
      sameAs: sameAs("password")
    }
  },
  methods: {
    login() {
      if (!this.$v.$invalid) {
        alert("Entrando...");
      } else {
        this.$v.$touch();
      }
    }
  }
};
</script>

<style scoped>
input {
  display: block;
}
p {
  color: red;
}
</style>

