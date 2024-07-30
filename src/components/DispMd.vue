<script setup>
import markdownit from 'markdown-it'
import axios from 'axios';

const props = defineProps({
    mdUrl: {
        type: String,
        required: true,
    }
});

let result = "";

const md = markdownit({
  html: true,
  linkify: true,
  typographer: true
})


try {
    const response = await axios.get(props.mdUrl);
    result = md.render(response.data);
} catch (error) {
    console.error('Failed to get MarkDown file:', error);
}

</script>

<template>
    <div v-html="result"></div>
</template>
