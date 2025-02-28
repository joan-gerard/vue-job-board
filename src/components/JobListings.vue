<script setup lang="ts">
import { reactive, defineProps, onMounted } from "vue"
import type { Job } from '@/types/global'
import JobListing from "@/components/JobListing.vue"
import { RouterLink } from "vue-router"
import axios from "axios"

defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }
})

const state = reactive({
    jobs: [],
    isLoading: true
})

onMounted(async () => {
    try {
        const response = await axios.get("http://localhost:8000/jobs");
        state.jobs = response.data
    } catch (error) {
        console.error("Error fetching data", error)
    } finally {
        state.isLoading = false
    }
})
</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-x lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" v-bind:key="(job as Job).id"
                    v-bind:job="job" />
            </div>
        </div>
    </section>
    <section class="m-auto max-w-lg my-10 px-6" v-if="showButton">
        <RouterLink to="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View
            All Jobs</RouterLink>
    </section>
</template>