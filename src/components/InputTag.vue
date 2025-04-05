<script>
export default {
  data() {
    return {
      currentValue: '',
      tags: [],
    }
  },

  methods: {
    // en uno validas la tecla que se presiona y en el otro validas el submit del form directamente
    handleKeyDown(e) {
      if (e.key === 'Backspace' && this.currentValue === '') {
        this.tags.pop()
      }
    },
    handleSubmit() {
      if (this.currentValue !== '') {
        const exists = this.tags.some((item) => item === this.currentValue)
        if (!exists) {
          this.tags.push(this.currentValue)
          this.currentValue = ''
        }
      }
    },
    deleteTag(tag) {
      this.tags = this.tags.filter((t) => t !== tag)
    },
  },
}
</script>

<template>
  <div class="inputTag">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }} <button @click="deleteTag(tag)">X</button>
      </div>
    </div>
    <form @submit.prevent="handleSubmit">
      <input type="text" v-model="currentValue" @keydown="handleKeyDown" />
    </form>
  </div>
</template>

<style scoped></style>
