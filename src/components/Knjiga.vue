<script setup>
const props = defineProps({
  naslov: String,
  autor: String,
  godina: Number,
  naslovnica: String,
});
const emit = defineEmits(["promjeni"]);
const promjena = (broj) => {
  emit("promjeni", broj);
};
</script>
<template>
  <div>
    <div>
      <img :src="naslovnica" alt="" class="naslovnica" />
    </div>
    <div><slot /> <b>Naslov: </b>{{ naslov }}</div>
    <div><b>Autor: </b> {{ autor }}</div>
    <div><b>Godina: </b> {{ godina }}</div>
    <button @click="promjena(-1)">Prethodna</button>
    <button @click="promjena(1)">Slijedeca</button>
  </div>
</template>
<style scoped>
.naslovnica {
  height: 300px;
}
</style>
