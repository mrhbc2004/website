<script setup>
import { ref, watch, onMounted } from 'vue';
import foode from 'food-e';

const props = defineProps({
    insCodes: {
        type: Array,
        required: true,
    },
    selectedINS: {
        type: Array,
        required: true,
    },
    addToSelectedINS: {
        type: Function,
        required: true,
    },
    clearSelectedINS: {
        type: Function,
        required: true,
    }
});

const localInsCodes = ref(props.insCodes);

onMounted(async () => {
    try {
        const additives = await foode('');

        if (Array.isArray(additives)) {
            const codes = additives.map(
                (additive) => `${additive.code} - ${additive.names.slice(0, 75)}`
            );
            localInsCodes.value = codes;
            props.insCodes.splice(0, props.insCodes.length, ...codes);
        } else {
            console.error('Unexpected data format:', additives);
        }
    } catch (error) {
        console.error('Failed to load food additives:', error);
    }
});

const handleSelectionChange = (items) => {
    console.log(items);
    items.forEach((item) => {
        console.log(props.selectedINS);
        props.addToSelectedINS(item);
    });
};

</script>

<template>
    <div>
        <v-combobox clearable chips multiple label="Search INS Codes" :items="insCodes"
            @update:model-value="handleSelectionChange" @click:clear="props.clearSelectedINS"></v-combobox>
    </div>
</template>
