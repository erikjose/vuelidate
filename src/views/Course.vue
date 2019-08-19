<template>
  <div>
    <ul>
      <li>
        <a href="#" @click.prevent="$v.$touch()">Touch()</a>
      </li>
      <li>
        <a href="#" @click.prevent="$v.$reset()">Reset()</a>
      </li>
    </ul>
    <form action>
      <label for="course">Curso:</label>
      <input
        v-model="name"
        @change="$v.name.$touch()"
        :class="{ 'fail-error' : $v.name.$error }"
        type="text"
        id="course"
      />
      <p class="error" v-if="$v.name.$error">Campo curso é requerido.</p>

      <label for="teacher">Professor:</label>
      <input
        v-model="teacher"
        @change="$v.teacher.$touch()"
        :class="{ 'fail-error' : $v.teacher.$error}"
        type="text"
        id="teacher"
      />
      <p class="error" v-if="$v.teacher.$error">Campo professor é requerido.</p>

      <p>Possui requisitos?</p>
      <div class="radios">
        <label for="yes">
          <input type="radio" v-model="req" name="req" :value="true" id="yes" />
          Sim
        </label>

        <label for="not">
          <input type="radio" v-model="req" name="req" :value="false" id="not" />
          Não
        </label>
      </div>

      <p class="error" v-if="$v.req.$error">Campo requisitos é requerido.</p>

      <div class="description" v-if="req">
        <label for="req">Descrição do requisitos:</label>
        <textarea
          v-model="description"
          :class="{ 'fail-error' :  $v.description.$error}"
          name="req"
          id="req"
          cols="40"
          rows="5"
          style="resize: none;"
        ></textarea>
      </div>

      <p class="error" v-if="$v.description.$error">Campo descrição é requerido.</p>

      <button @click.prevent="addClass()">Adicionar aula +</button>

      <div class="class">
        <div
          class="class-container"
          v-for="(aula, index) in $v.classroom.$each.$iter"
          :key="aula.id"
        >
          <input
            type="text"
            :class="{ 'fail-error' : aula.name.$error }"
            v-model="aula.name.$model"
            name="class"
            placeholder="Nome da aula"
          />
          <img
            :src="require('@/assets/warning.svg')"
            v-if="aula.name.$error"
            alt="Error"
            width="15"
          />
          <span @click.prevent="removeClass(index)">&times;</span>
        </div>
      </div>

      <button type="submit" @click.prevent="$v.$invalid ? $v.$touch() : login()">Cadastrar curso</button>
    </form>
  </div>
</template>

<script>
import { required, requiredIf } from "vuelidate/lib/validators";

export default {
  name: "course",
  data: () => ({
    name: "",
    teacher: "",
    req: "",
    description: "",
    classroom: [],
    id: 0
  }),
  validations: {
    name: { required },
    teacher: { required },
    req: { required },
    description: {
      required: requiredIf(function() {
        return this.req;
      })
    },
    classroom: {
      $each: {
        name: { required }
      }
    }
  },
  methods: {
    login() {
      alert("oi, vc criou um curso!!!");
      this.$v.$reset();
      this.classroom = [];
      this.name = "";
      this.teacher = "";
      this.req = "";
      this.description = "";
    },
    addClass() {
      this.id += 1;
      this.classroom.push({
        id: this.id,
        name: ""
      });
    },
    removeClass(index) {
      this.classroom.splice(index, 1);
    }
  }
};
</script>

<style>
input,
label {
  display: block;
}
button {
  display: block;
  margin-top: 15px;
}
.radios {
  margin-bottom: 15px;
}
.radios label {
  display: flex;
}
.class {
  margin-top: 15px;
}
.class-container {
  display: flex;
}
.class-container img {
  margin-left: 20px;
  margin-top: -15px;
}
.class-container input {
  margin-bottom: 15px;
  height: 25px;
  width: 250px;
}
.class-container span {
  margin-left: 20px;
  font-size: 24px;
  cursor: pointer;
}
p.error {
  color: red;
}
.fail-error {
  border: 1px solid red;
}
</style>