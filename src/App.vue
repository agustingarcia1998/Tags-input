<script setup>
import InputTag from './components/InputTag.vue'

const handleOnTagsChange = (tags) => {
  console.log(tags)
}
</script>

<template>
  <InputTag @onTagsChange="handleOnTagsChange" />
</template>

<style scoped></style>
