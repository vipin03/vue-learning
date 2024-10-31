<template>
    <Hero title="Hey title from props" subtitle="subtitle from props"/>
    <HomeCards />
    <JobListings :limit="3" :showButton="true"/>
</template>
<script setup>
import Hero from '../components/Hero.vue';
import HomeCards from '../components/HomeCards.vue';
import JobListings from '../components/JobListings.vue';
</script>