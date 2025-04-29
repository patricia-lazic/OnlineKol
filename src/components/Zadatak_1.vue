<script setup>
import { ref, computed } from "vue";
const email = ref("");
const lozinka = ref("");
const ponovi_lozinku = ref("");
const provjeraEmaila = () => {
  if (!email.value.includes("@")) {
    return 1;
  }
  if (email.value[0] === "@") {
    return 2;
  }
  if (
    !email.value.includes("unipu.hr") ||
    !email.value.includes("student.unipu.hr")
  ) {
    return 3;
  }
  if (
    email.value.includes("@") &&
    email.value[0] !== "@" &&
    (email.value.includes("unipu.hr") ||
      email.value.includes("student.unipu.hr"))
  ) {
    return 4;
  }
};
const provjeraLozinke = computed(() => {
  if (!/[A-Z]/.test(lozinka.value)) {
    return "Lozinka mora imati barem jedno veliko slovo!";
  }
  if (lozinka.value.length < 8) {
    return "Lozinka mora imati najmanje 8 znakova!";
  }
  if (/[A-Z]/.test(lozinka.value) && lozinka.value.length > 8) {
    return "Lozinka je validna";
  }
});
</script>

<template>
  <div></div>
  <div>
    <input v-model="email" />
    <div v-if="provjeraEmaila() === 1">Email treba sadržavati "@" simbol</div>
    <div v-if="provjeraEmaila() === 2">
      Email se treba sastojati od lokalnog djela i domene!
    </div>
    <div v-if="provjeraEmaila() === 3">
      Email treba zavrsiti s "unipu.hr" ili "student.unipu.hr"
    </div>
    <div v-if="provjeraEmaila() === 4">Email je validan!</div>
  </div>
  <div>
    <input type="password" v-model="lozinka" />
    {{ provjeraLozinke }}
  </div>
  <div><input type="password" v-model="ponovi_lozinku" /></div>
  <div v-if="lozinka !== ponovi_lozinku">Lozinke se ne podudaraju!"</div>
  <div v-else>Lozinke se podudaraju</div>
</template>

<style scoped></style>
