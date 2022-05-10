<template>
  <div>
    <h2>Jokes Page</h2>
    <SearchJokes @search-text="searchText" />
    <Joke 
      v-for="joke in jokes"
      :key="joke.id"
      :id="joke.id"
      :joke="joke.joke"

      />
  </div>
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke.vue'
import SearchJokes from '../../components/SearchJokes.vue'

export default {
  data() {
    return {
      jokes: []
    }
  },
  components: { Joke, SearchJokes },
  async created() {
    const config = {
      headers: {
        'Accept': 'application/json'
      }
    }
    try {
      const res = await axios.get('https://icanhazdadjoke.com/search', config)
      this.jokes = res.data.results
      console.log(this.jokes);
    } catch (err) {
      console.log(err);      
    }
  },
  methods: {
    async searchText(text) {
      console.log(text);
      const config = {
      headers: {
        'Accept': 'application/json'
      }
    }
    try {
      const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config)
      this.jokes = res.data.results
      console.log(this.jokes);
    } catch (err) {
      console.log(err);      
    }
    }
  },
  head() {
    return {
      title: 'Jokes on Me',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'My life is a joke'
        }
      ]
    }
  }
}
</script>

<style>

</style>