<template>
    <div>
        <h1> {{ part.title }}</h1>
        <div>{{ part.description }}</div>
    </div>
</template>

<script setup>
import { computed } from 'vue';
import parts from '../data/parts';

const props = defineProps(['partType', 'id']);
const part = computed(() => parts[props.partType].find((part1) => part1.id === +props.id));
</script>
