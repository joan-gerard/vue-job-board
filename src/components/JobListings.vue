<script setup lang="ts">
import jobData from "@/jobs.json"
import { ref } from "vue"
import type { Job } from '@/types/globalTypes'
import JobListing from "@/components/JobListing.vue"

const jobs = ref<Job[]>(jobData)

</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-x lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in jobs" v-bind:key="job.id" v-bind:job="job" />
            </div>
        </div>
    </section>
</template>