<script setup>
import Tiptap from '../components/Tiptap.vue'
</script>

<template>
  <main>
    {{ $route.params.id }}
    <Tiptap />
  </main>
</template>
