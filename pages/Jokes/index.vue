<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import Joke from '../../components/Joke';
import SearchJokes from '../../components/SearchJokes';

export default {
  components: {
    Joke,
    SearchJokes
  },
  async asyncData({ $axios }) {
    const config = { headers: { 'Accept': 'application/json' } };
    let res = [];
    try {
      res = await $axios.$get('https://icanhazdadjoke.com/search', config);
    } catch (err) {
      console.log(err);
    }
    return {
      jokes: res.results
    }
  },
  methods: {
    async searchText(text) {
      const config = { headers: { 'Accept': 'application/json' } };
      let res = Object;
      try {
        res = await this.$axios.$get(`https://icanhazdadjoke.com/search?term=${text}`, config);
      } catch (err) {
        console.log(err);
      }
      this.jokes = res.results;
    }
  },
  head() {
    return {
      title: 'Dad Jokes',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best place for corny dad jokes'
        }
      ]
    }
  }
}
</script>

<style>

</style>
