<script setup>
defineProps(['name', 'url']);
</script>

<template>
    <div class="container">
        <h3>{{ name }}</h3>
        <h5>{{ url }}</h5>
    </div>
</template>
