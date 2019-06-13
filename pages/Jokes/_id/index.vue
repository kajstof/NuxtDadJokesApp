<template>
  <div>
    <nuxt-link to="/jokes">Back to Jokes</nuxt-link>
    <h2>{{ joke }}</h2>
    <hr />
    <small>Joke ID: {{ $route.params.id }}</small>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    const config = { headers: { 'Accept': 'application/json' } };
    console.log();
    let res = Object;
    try {
      res = await $axios.$get(`https://icanhazdadjoke.com/j/${params.id}`, config);
    } catch (err) {
      console.log(err);
    }
    return {
      joke: res.joke
    }
  },
  head() {
    return {
      title: this.joke,
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
