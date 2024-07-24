<script setup>
import { ref, watch } from 'vue'

const items = [
    {
        title: 'Foo',
        value: 'foo',
    },
    {
        title: 'Bar',
        value: 'bar',
    },
    {
        title: 'Fizz',
        value: 'fizz',
    },
    {
        title: 'Buzz',
        value: 'buzz',
    },
]

const drawer = ref(false)
const group = ref(null)

watch(group, () => {
    drawer.value = false
})
</script>

<template>
    <div>
        <v-app-bar :elevation="1">
            <template v-slot:prepend>
                <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
            </template>

            <v-app-bar-title>is it healthy?</v-app-bar-title>

            <template v-slot:append>
                <v-btn icon="mdi-camera"></v-btn>

                <v-btn icon="mdi-magnify"></v-btn>

                <v-btn icon="mdi-dots-vertical"></v-btn>
            </template>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" :location="$vuetify.display.mobile ? 'bottom' : undefined" temporary>
            <v-list :items="items"></v-list>
        </v-navigation-drawer>
    </div>
</template>