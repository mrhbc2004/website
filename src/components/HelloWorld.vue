<script setup>
import { ref } from 'vue';

import ImageOCR from './search/ImageOCR.vue';
import SearchBar from './search/SearchBar.vue';
import FoodInfo from './search/FoodInfo.vue';
import ins from "../data/ins.json"

const insCodes = ref(ins);
const selectedINS = ref([]);

const addToSelectedINS = (item) => {
  if (!selectedINS.value.includes(item)) {
    selectedINS.value.push(item);
  }
};

const clearSelectedINS = () => {
  selectedINS.value = [];
};
</script>


<template>
  <v-container>
    <v-responsive class="mx-auto" max-width="900">

      <!-- <h2>{{ selectedINS }}</h2> -->
      <ImageOCR :insCodes="insCodes" :selectedINS="selectedINS" :addToSelectedINS="addToSelectedINS"
        :clearSelectedINS="clearSelectedINS" />
      <SearchBar :insCodes="insCodes" :selectedINS="selectedINS" :addToSelectedINS="addToSelectedINS"
        :clearSelectedINS="clearSelectedINS" />

      <FoodInfo v-for="inscode in selectedINS" :inscode="inscode" />

    </v-responsive>
  </v-container>
</template>
