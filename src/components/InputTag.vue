<script>
export default {
  emits: ['onTagsChange'],
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
        // this.onTagsChange(this.tags)
        this.$emit('onTagsChange', this.tags)
      }
    },
    handleSubmit() {
      if (this.currentValue !== '') {
        const exists = this.tags.some((item) => item === this.currentValue)
        if (!exists) {
          this.tags.push(this.currentValue)
          this.currentValue = ''
          //   this.onTagsChange(this.tags)
          this.$emit('onTagsChange', this.tags)
        }
      }
    },
    deleteTag(tag) {
      this.tags = this.tags.filter((t) => t !== tag)
      //   this.onTagsChange(this.tags)
      this.$emit('onTagsChange', this.tags)
    },
  },
}
</script>

<template>
  <div class="tagsContainer">
    <div class="title">TAGS APP</div>
    <!-- 🔹 TÍTULO -->
    <div class="inputTag">
      <div class="tags">
        <div class="tag" v-for="(tag, index) in tags" :key="index">
          {{ tag }} <button @click="deleteTag(tag)">X</button>
        </div>
      </div>
      <form @submit.prevent="handleSubmit">
        <input class="input" type="text" v-model="currentValue" @keydown="handleKeyDown" />
      </form>
    </div>
  </div>
</template>

<style scoped>
.title {
  position: absolute;
  top: 20px;
  width: 100%;
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  color: #000;
  background-color: rgb(159, 241, 120);
  padding: 10px 0;
}

.tagsContainer {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: rgb(159, 241, 120);
}
.inputTag {
  display: inline-flex;
  border: solid 1px #000;
  border-radius: 3px;
  height: 43px;
  background-color: white;
}

.tags {
  display: flex;
  gap: 3px;
  padding: 5px;
}

.tags .tag {
  display: flex;
  padding: 5px;
  border: solid 2px #020202;
  gap: 5px;
  align-content: center;
  border-radius: 10px;
}

.inputTag form {
  display: inline-flex;
}

.inputTag .input {
  border: none;
  outline: none;
  padding: 0 5px;
}

.inputTag button {
  background-color: transparent;
  border: none;
  border-radius: 3px;
}

.inputTag button:hover {
  background-color: #eee;
}
</style>
