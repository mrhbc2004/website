<script setup>
import { ref } from 'vue'

const drawer = ref(null)
</script>

<template>
    <div>
        <v-app-bar :elevation="1">
            <template v-slot:prepend>
                <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
            </template>

            <v-app-bar-title>is it healthy?</v-app-bar-title>
            <v-spacer></v-spacer>
            <template v-slot:append>
                <v-btn icon="mdi-camera"></v-btn>
                <v-btn icon="mdi-magnify"></v-btn>
                <v-btn icon="mdi-dots-vertical"></v-btn>
            </template>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" temporary>
            <v-list-item 
                title="Hirusha Adikari"
                prepend-icon="mdi-account"
                class="mt-3 mb-2"
            ></v-list-item>

            <v-divider></v-divider>

            <v-list density="compact" nav>
                <v-list-item prepend-icon="mdi-magnify" title="Lookup" value="home"></v-list-item>
                <v-list-item prepend-icon="mdi-history" title="History" value="history"></v-list-item>
                <v-list-item prepend-icon="mdi-wrench" title="API Keys" value="apikeys"></v-list-item>
                <v-list-item prepend-icon="mdi-cog" title="Account" value="about"></v-list-item>
                <v-list-item prepend-icon="mdi-exit-to-app" title="Log Out" value="logout"></v-list-item>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>