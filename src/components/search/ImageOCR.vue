<script setup>
import { ref } from 'vue';
import Tesseract from 'tesseract.js';

const fileInput = ref(null);
const imageSrc = ref('');
const ocrResult = ref('');

const selectImage = () => {
    console.log("foo running");
    fileInput.value.click();
};

const handleFileChange = (event) => {
    const file = event.target.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
            imageSrc.value = e.target.result;
            performOCR(e.target.result);
        };
        reader.readAsDataURL(file);
    }
};

const performOCR = (image) => {
    Tesseract.recognize(
        image,
        'eng',
        {
            logger: (m) => console.log(m),
        }
    ).then(({ data: { text } }) => {
        ocrResult.value = text;
    }).catch((error) => {
        console.error(error);
    });
};

</script>

<template>
    <div>
        <button @click="selectImage">Take or Upload Picture</button>
        <input type="file" ref="fileInput" accept="image/*" @change="handleFileChange" style="display: none">
        <div v-if="imageSrc">
            <img :src="imageSrc" alt="Selected Image" style="max-width: 100%; margin-top: 20px;">
        </div>
        <div v-if="ocrResult">
            <h3>OCR Result:</h3>
            <p>{{ ocrResult }}</p>
        </div>
    </div>
</template>

<style scoped>
button {
    margin: 10px 0;
}
</style>