<template>
  <header class="header">
    <div v-for="(string) in arr" :key="string.name">
      {{string.name}}
    </div>
  </header>
</template>

<script lang="ts" setup>
import {ref} from "vue";

const arr = ref([
  {
    idx: 0,
    name: "lss",
    age: 29
  },
  {
    idx: 1,
    name: "lsg",
    age: 29
  },
  {
    idx: 2,
    name: "lsh",
    age: 54
  },
]);

</script>

<style lang="scss" scoped>
@import "@/assets/scss/components/header/header.scss";
</style>