<script setup>
const { data: count } = await useFetch("http://localhost:3001/flight-m");
</script>
<template>
  <p>{{count}}</p>
</template>