<script setup>

import { ref } from 'vue'

const props = defineProps({
    inscode: Object,
});

const show = ref(false)

</script>

<template>
    <v-card :prepend-icon="props.inscode.icon" max-width="600">
        <template v-slot:title>
            <span class="font-weight-black overflow-below"> {{ props.inscode.display_name }}</span>
        </template>

        <v-card-subtitle class="overflow-below">
            {{ props.inscode.type }}
        </v-card-subtitle>

        <v-card-text>
            <p><strong>Origin:</strong> {{ props.inscode.more_info.origin }}</p>
            <p><strong>Characteristics:</strong> {{ props.inscode.more_info.characteristics }}</p>
            <p><strong>Daily Intake:</strong> {{ props.inscode.more_info.daily_intake }}</p>
            <p><strong>Side Effects:</strong> {{ props.inscode.more_info.side_effects }}</p>



        </v-card-text>

        <v-card-actions>
            <p>Origin</p>
            <!-- <v-btn color="orange-lighten-2" text="Explore"></v-btn> -->

            <v-spacer></v-spacer>

            <v-btn :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="show = !show"></v-btn>
        </v-card-actions>

        <v-expand-transition>
            <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                    I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time
                    for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data
                    file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got
                    to find a way to escape.
                </v-card-text>
            </div>
        </v-expand-transition>
        <!-- 
        <div class="buttons-container">
            <div v-if="props.inscode.more_info.articles">
                <div v-for="(url, name) in props.inscode.more_info.articles" :key="name" class="button-wrapper">
                    <a :href="url" target="_blank">
                        <v-btn color="purple-accent-2 pt-0" variant="text">{{ name }}</v-btn>
                    </a>
                </div>
            </div>
        </div> -->

        <v-card-actions class="pt-0">
            <v-row no-gutters>
                <v-col v-for="(url, name) in props.inscode.more_info.articles" :key="name" cols="auto" class="mb-2">
                    <v-btn :href="url" target="_blank" color="purple-accent-2" variant="text" class="mx-1">
                        {{ name }}
                    </v-btn>
                </v-col>
            </v-row>
        </v-card-actions>
    </v-card>
</template>

<style scoped>
.overflow-below {
    white-space: normal;
    overflow: visible;
}
</style>