<script setup>
import { ref } from 'vue'

const drawer = ref(null)
</script>

<template>
    <div>
        <v-app-bar :elevation="1">
            <template v-slot:prepend>
                <!-- <v-app-bar-nav-icon ></v-app-bar-nav-icon> -->
            </template>
            <v-app-bar-title>is it healthy?</v-app-bar-title>
            <v-spacer></v-spacer>
            <template v-slot:append>
                <v-btn icon="mdi-magnify"></v-btn>
                <v-btn icon="mdi-help-circle-outline"></v-btn>
                <v-btn icon="mdi-menu" @click.stop="drawer = !drawer"></v-btn>
            </template>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" temporary location="left">
            <v-list-item 
                title="by Hirusha Adikari"
                prepend-icon="mdi-account"
                class="mt-3 mb-2"
            ></v-list-item>

            <v-divider></v-divider>

            <v-list density="compact" nav>
                <v-list-item prepend-icon="mdi-magnify" title="Lookup" value="home"></v-list-item>
                <v-list-item prepend-icon="mdi-help" title="Help & Support" value="help"></v-list-item>
                <v-list-item prepend-icon="mdi-head-question-outline" title="How it works?" value="how"></v-list-item>
                <v-divider></v-divider>
                <v-list-item prepend-icon="mdi-license" title="License" value="license"></v-list-item>
                <v-list-item prepend-icon="mdi-open-source-initiative" title="Open Srouce Licenses" value="license_oss"></v-list-item>
                <v-list-item prepend-icon="mdi-xml" title="Contribute Code" value="contribute_code"></v-list-item>
                <v-list-item prepend-icon="mdi-medical-bag" title="Contibute Data" value="contribute_data"></v-list-item>
                <v-list-item prepend-icon="mdi-account-group-outline" title="Contributors" value="logout"></v-list-item>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>