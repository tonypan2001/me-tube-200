<template>
    <h1 class="text-3xl">
        Add Artist
    </h1>

    <form class="m-4" @submit.prevent="onSubmit()">
        <div>
            <label for="name">Artist Name</label>
            <p class="text-red-600" v-if="formErrors.errors">
                {{ formErrors.errors }}
            </p>
            <input class="border border-gray-400 p-2 ml-2 rounded-xl" 
            v-model="formData.name"
            placeholder="Artist name"
            type="text" id="name">
        </div>
        <div class="mt-4">
            <button class="px-4 py-2 border bg-blue-300 rounded-xl" type="submit">
                Submit
            </button>
        </div>
    </form>


</template>

<script setup lang="ts">
const formData = ref({
    name: ""
})

const formErrors = ref({
    errors: null
})

async function onSubmit() {
    const { name } = formData.value

    const { data: response, error } = await useFetch<any>(
        "http://localhost/api/artist", {
            method: "POST",
            body: { name }
        }
    )

    if (response.value !== null) {
        await navigateTo(`/artists/${response.value.id}`)
    } else {
        console.log(error)
        const { message } = error.value!.data // ! บอกว่า property นี้ไม่เป็น null แน่ ๆ
        formErrors.value.errors = message;
    }
}

</script>