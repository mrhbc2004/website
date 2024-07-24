<script setup>

import { ref } from 'vue'
import { fa } from 'vuetify/locale';

const props = defineProps({
    inscode: Object,
});

const show = ref(
    {
        origin: false,
        daily_intake: false,
        side_effects: true,
        uses: false,
        precautions: false,
        overview: false,
        interactions: false,
    }
)

const formattedContent = (key) => {
    return computed(() => {
        // Replace \n with <br><br>
        return props.inscode.more_info[key].replace(/\n/g, '<br><br>');
    }).value;
};

</script>

<template>
    <v-card :prepend-icon="props.inscode.icon" max-width="600">
        <template v-slot:title>
            <span class="font-weight-black overflow-below"> {{ props.inscode.display_name }}</span>
        </template>

        <v-card-subtitle class="overflow-below">
            <p>
                {{ props.inscode.names }}
            </p>
        </v-card-subtitle>

        <v-card-text>
            This is a {{ props.inscode.type }}
        </v-card-text>

        <!-- Side Effects -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Side Effects</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.side_effects ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                @click="show.side_effects = !show.side_effects"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.side_effects">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('side_effects')"></v-card-text>
            </div>
        </v-expand-transition>

        <!-- Overview -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Overview</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.overview ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                @click="show.overview = !show.overview"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.overview">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('overview')"></v-card-text>
            </div>
        </v-expand-transition>

        <!-- Uses -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Uses</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.uses ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="show.uses = !show.uses"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.uses">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('uses')"></v-card-text>
            </div>
        </v-expand-transition>

        <!-- Precautions -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Precautions</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.precautions ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                @click="show.precautions = !show.precautions"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.precautions">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('precautions')"></v-card-text>
            </div>
        </v-expand-transition>

        <!-- Interactions -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Interactions</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.interactions ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                @click="show.interactions = !show.interactions"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.interactions">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('interactions')"></v-card-text>
            </div>
        </v-expand-transition>

        <!-- Origin -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Origin</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.origin ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                @click="show.origin = !show.origin"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.origin">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('origin')"></v-card-text>
            </div>
        </v-expand-transition>

        <!-- Daily Intake -->
        <v-card-actions class="highlight-on-hover">
            <p class="ml-2 font-weight-bold text-h6">Daily Intake</p>
            <v-spacer></v-spacer>
            <v-btn :icon="show.daily_intake ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                @click="show.daily_intake = !show.daily_intake"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show.daily_intake">
                <v-divider></v-divider>
                <v-card-text v-html="formattedContent('daily_intake')"></v-card-text>
            </div>
        </v-expand-transition>

        <v-card-actions class="pt-0">
            <v-row no-gutters>
                <v-col v-for="(url, name) in props.inscode.more_info.articles" :key="name" cols="auto" class="mb-2">
                    <v-btn :href="url" target="_blank" color="purple-accent-2" variant="text" class="mx-1">
                        &nearr; {{ name }}
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

.highlight-on-hover {
    transition: background-color 0.3s ease;
}

.highlight-on-hover:hover {
    background-color: var(--v-theme-surface-light);
}
</style>