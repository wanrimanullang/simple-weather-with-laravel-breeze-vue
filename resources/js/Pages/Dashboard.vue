<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import Weather from '../Components/Wheater.vue'
</script>

<template>
    <Head title="Dashboard" />
    <AuthenticatedLayout>

        <div id="app">
            <Weather city="Jakarta"></Weather>
        </div>
    </AuthenticatedLayout>
</template>
