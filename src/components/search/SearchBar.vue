<script setup>

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


const handleSelectionChange = (items) => {
    props.clearSelectedINS();
    items.forEach((item) => {
        props.addToSelectedINS(item);
    });
};

// console.log(props.insCodes);

</script>

<template>
    <div>
        <v-combobox clearable chips multiple label="Search INS Codes" :items="props.insCodes" item-value="code"
            item-title="name" @update:model-value="handleSelectionChange"></v-combobox>
    </div>
</template>
