<script setup>
import { ref } from 'vue';

import ImageOCR from './search/ImageOCR.vue';
import SearchBar from './search/SearchBar.vue';
import FoodInfo from './search/FoodInfo.vue';
import axios from "axios"
import { useRouter } from 'vue-router';


const DATA_SUMMARY = 'https://raw.githubusercontent.com/is-it-healthy/data/v2/dist/ins-summary.json';


const router = useRouter();


const selectedINS = ref([]);
const insCodes = ref([]);
const dlgErrSummaryShow = ref(false);
const dlgErrSummaryError = ref('');

onMounted(async () => {
  try {
    const response = await axios.get(DATA_SUMMARY);
    insCodes.value = response.data
  } catch (error) {
    console.error('Failed to load INS codes summary list:', error);
    dlgErrSummaryShow.value = true;
    dlgErrSummaryError.value = ` ${error}`
  }
});

const addToSelectedINS = (item) => {
  if (!selectedINS.value.includes(item)) {
    selectedINS.value.push(item);
  }
};

const clearSelectedINS = () => {
  selectedINS.value = [];
};

const goBack = () => {
  router.go(-1);
};

const retry = () => {
  window.location.reload();
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

      <!-- <FoodInfo v-for="inscode in selectedINS" :inscode="inscode" /> -->
      <v-row>
        <v-col v-for="inscode in selectedINS" :key="inscode.code" cols="12" sm="6" md="6">
          <FoodInfo :inscode="inscode" />
        </v-col>
      </v-row>

    </v-responsive>

    <v-dialog v-model="dlgErrSummaryShow" width="auto" persistent>
      <v-card max-width="400" prepend-icon="mdi-alert-circle" title="An error has occured!"
        :text="`Failed to load the summary list from the backend. Cannot connect to the server. Error: ${dlgErrSummaryError}`">
        <template v-slot:actions>
          <v-spacer></v-spacer>
          <!-- @click="dlgErrSummaryShow = false" -->
          <v-btn class="ms-auto" text="Go back" @click="goBack"></v-btn>
          <v-btn class="ms-auto" text="Retry" @click="retry"></v-btn>
        </template>
      </v-card>
    </v-dialog>
  </v-container>
</template>
