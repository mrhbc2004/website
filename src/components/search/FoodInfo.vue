<script setup>

const props = defineProps({
    inscode: Object,
});

</script>

<template>
    <div>
        <br>
        <v-card class="mx-auto" prepend-icon="$vuetify" :subtitle="`${props.inscode.code} - ${props.inscode.names}`" width="400">
            <template v-slot:title>
                <span class="font-weight-black">{{ props.inscode.display_name }}</span>
            </template>

            <v-card-text class="bg-surface-light pt-4">
                Lorem ipsum dolor sit samet consectetur adipisicing elit. Commodi, ratione debitis quis est labore
                voluptatibus!
                Eaque cupiditate minima, at placeat totam, magni doloremque veniam neque porro libero rerum unde
                voluptatem!
            </v-card-text>
        </v-card>
    </div>
</template>