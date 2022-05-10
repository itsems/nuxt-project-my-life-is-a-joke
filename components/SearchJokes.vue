<template>
  <form class="search" @submit.prevent="onSubmit">
    <input type="text" v-model="text" placeholder="Search Jokes...">
    <input type="submit" value="Search Jokes">
  </form>
  
</template>

<script>
export default {
  name: 'SearchJokes',
  data() {
    return {
      text: ''
    }
  },
  methods: {
    onSubmit() {
      this.$emit('search-text', this.text)
      this.text = "";
    }
  }
}
</script>

<style>
.search {
  margin-bottom: 15px;
  margin-left: 20px;
}
</style>