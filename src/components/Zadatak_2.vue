<script setup>
import { computed, ref } from "vue";

const mobiteli = ref([
  {
    marka: "Apple",
    model: "iPhone 15",
    cijena: 1000,
    funcionalnosti: ["Face ID", "Bixby"],
  },
  {
    marka: "Samsung",
    model: "Galaxy S22",
    cijena: 900,
    funcionalnosti: ["Bixby", "Samsung Pay"],
  },
  {
    marka: "Google",
    model: "Pixel 8",
    cijena: 850,
    funcionalnosti: ["Google Assistant"],
  },
  {
    marka: "Samsung",
    model: "Galaxy Z Fold 5",
    cijena: 1800,
    funcionalnosti: ["Apple Pay", "S Pen", "DeX"],
  },
]);

const sortiraniMobiteli = computed(() => {
  return mobiteli.value.sort((a, b) => b.cijena - a.cijena);
});

const iphone_funkcionalnosti = ["Face ID", "Apple Pay", "Siri", "AirDrop"];
const samsung_funkcionalnosti = ["Samsung Pay", "Bixby", "DeX", "S Pen"];
const novaCijena = ref(0);
const azurirajCijenu = (mobitelIndex) => {
  sortiraniMobiteli.value[mobitelIndex].cijena = novaCijena.value;
};
const validneMarke = ["Apple", "Samsung"];
const validneFunkcionalnosti = ref([]);
const provjeriFunkcionalnost = (index, funkIndex) => {
  const mobitel = sortiraniMobiteli.value[index];
  const funkcionalnost = mobitel.funcionalnosti[funkIndex];
  if (mobitel.marka === "Apple") {
    if (iphone_funkcionalnosti.includes(funkcionalnost)) {
      validneFunkcionalnosti.value.push([index, funkIndex, true]);
    } else {
      validneFunkcionalnosti.value.push([index, funkIndex, false]);
    }
  } else if (mobitel.marka === "Samsung") {
    if (samsung_funkcionalnosti.includes(funkcionalnost)) {
      validneFunkcionalnosti.value.push([index, funkIndex, true]);
    } else {
      validneFunkcionalnosti.value.push([index, funkIndex, false]);
    }
  }

  return false;
};
const getLogo = (index) => {
  const mobitel = sortiraniMobiteli.value[index];
  if (mobitel.marka === "Apple") {
    return "🍎";
  }
  if (mobitel.marka === "Samsung") {
    return "🔵";
  }

  return "❓";
};
</script>

<template>
  <div>
    <div v-for="(item, index) in sortiraniMobiteli" :key="index">
      {{ getLogo(index) }} Marka: {{ item.marka }} Model:
      {{ item.model }} cijena: {{ item.cijena }}
      <button @click="azurirajCijenu(index)">Ažuriraj</button>
      funcionalnosti
      <li v-for="(funk, funkIndex) in item.funcionalnosti">
        {{ funk }}
        <span v-if="validneMarke.includes(item.marka)">
          <button
            v-if="
              !validneFunkcionalnosti.find(
                (vf) => vf[0] === index && vf[1] === funkIndex
              )
            "
            @click="provjeriFunkcionalnost(index, funkIndex)"
          >
            Provjeri
          </button>
          <span v-else>
            <span
              v-if="
                validneFunkcionalnosti.find(
                  (vf) => vf[0] === index && vf[1] === funkIndex && vf[2]
                )
              "
              >✅
            </span>
            <span v-else> ❌ </span>
          </span>
        </span>
        <span v-else><b>*Provjera nije moguća*</b> </span>
      </li>
    </div>
  </div>
  <div>Nova cijena: <input type="number" v-model="novaCijena" /></div>
</template>

<style scoped></style>
