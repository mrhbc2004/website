<script setup>
import { ref, onMounted } from 'vue';
import foode from 'food-e';
const insCodes = ref([]);

onMounted(async () => {
    try {
        const additives = await foode('');

        // ensure a list is returned
        if (Array.isArray(additives)) {
            insCodes.value = additives.map(additive => additive.code);
        } else {
            console.error('Unexpected data format:', additives);

        }
    } catch (error) {
        console.error('Failed to load food additives:', error);
    }
});
</script>

<template>
    <div>
        <v-combobox clearable chips multiple label="Search INS Codes" :items="insCodes"></v-combobox>
    </div>
</template>
