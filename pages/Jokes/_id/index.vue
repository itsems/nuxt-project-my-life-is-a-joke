<template>
  <div>
    <h3>{{ joke }}</h3>
    <small>joke id: {{ $route.params.id }}</small>
    <nuxt-link to="/jokes">Back</nuxt-link>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      joke: {}
    }
  },
  async created() {
    const config = {
      headers: {
        'Accept': 'application/json'
      }
    }
    try {
      const res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config)
      this.joke = res.data.joke;
      console.log(this.joke);
    } catch (err) {
      console.log(err);      
    }
  },
  head() {
    return {
      title: this.joke,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.joke
        }
      ]
    }
  }
}
</script>

<style>

</style>