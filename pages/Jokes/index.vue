<template>
  <div>
    <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import Joke from '../../components/Joke';
export default {
  components: {
    Joke
  },
  async asyncData({ $axios }) {
    const ip = await $axios.$get('http://icanhazip.com');
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
