<template>
    <h1>Artist</h1>

    <div v-if="pending">
        Loading...
    </div>
    <div v-else>
        <div class="mx-8 my-2 border p-4 rounded-xl hover:bg-green-200" 
            v-for="artist in artists" :key="artist.id">

            <nuxt-link class="hover:text-blue-500 hover:font-bold"
                :to="`/artists/${artist.id}`">

                {{ artist.name }}

            </nuxt-link>

        </div>
    </div>

</template>

<script setup lang="ts">
const { data: artists, pending } = await useLazyFetch<any>("http://localhost/api/artist")

console.log(artists.value)

</script>