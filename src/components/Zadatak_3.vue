<script setup>
import { ref } from "vue";
import Knjiga from "./Knjiga.vue";
const aktivnaKnjiga = ref(0);
const knjige = [
  {
    autor: "J. K. Rowling",
    godina: 1997,
    naslov: "Harry Potter and the Sorcerer's Stone",
    naslovnica: "src/assets/slike/Harry Potter and the Sorcerer's Stone.jpg",
  },
  {
    autor: "George Orwell",
    godina: 1949,
    naslov: "1984",
    naslovnica: "src/assets/slike/1984.jpg",
  },
  {
    autor: "Harper Lee",
    godina: 1960,
    naslov: "To Kill a Mockingbird",
    naslovnica: "/src/assets/slike/To Kill a Mockingbird.jpg",
  },
  {
    autor: "J.R.R. Tolkien",
    godina: 1954,
    naslov: "The Fellowship of the Ring",
    naslovnica: "/src/assets/slike/The Fellowship of the Ring.jpg",
  },
];
const promjeni = (broj) => {
  let noviIndex = aktivnaKnjiga.value + broj;
  if (noviIndex < 0) {
    noviIndex = knjige.length - 1;
  } else if (noviIndex > knjige.length - 1) {
    noviIndex = 0;
  }
  aktivnaKnjiga.value = noviIndex;
};
</script>

<template>
  <div>
    <Knjiga
      :autor="knjige[aktivnaKnjiga].autor"
      :godina="knjige[aktivnaKnjiga].godina"
      :naslov="knjige[aktivnaKnjiga].naslov"
      :naslovnica="knjige[aktivnaKnjiga].naslovnica"
      @promjeni="promjeni"
    >
      {{ aktivnaKnjiga + 1 }}.
    </Knjiga>
  </div>
</template>

<style scoped></style>
