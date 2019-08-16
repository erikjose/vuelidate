<template>
  <div>
    <form action>
      <label for="course">Courso:</label>
      <input type="text" id="course" />

      <label for="teacher">Professor:</label>
      <input type="text" id="teacher" />

      <p>Possui requerimentos?</p>
      <div class="radios">
        <label for="yes">
          <input type="radio" name="req" value="true" id="yes" />
          Sim
        </label>

        <label for="not">
          <input type="radio" name="req" value="false" id="not" />
          Não
        </label>
      </div>

      <label for="req">Qual?</label>
      <textarea name="req" id="req" cols="40" rows="5" style="resize: none;"></textarea>

      <button>Adicionar aula</button>

      <div class="class">
        <div class="class-container">
          <input type="text" name="class" id placeholder="Nome da aula" />
          <span>&times;</span>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";

export default {
  name: "course"
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
.class-container span {
  margin-left: 20px;
  font-size: 24px;
  cursor: pointer;
}
</style>