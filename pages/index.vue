<template>
  <div>
    <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>
      <h1>Nuxt Mountains</h1>
      <p>Just Testing</p>
      <nuxt-img src="/goat.png" alt="goat" sizes="md:15vw" format="webp" />
      <ul>
        <li v-for="mountain of mountains" :key="mountain">
          <h1>{{ mountain.title }}</h1>
          <!-- <img :src="mountain.image"> -->
          <!-- <nuxt-img :src="mountain.image" /> -->
          <nuxt-img :src="mountain.image" format="webp" placeholder />
        </li>
      </ul>
      <button @click="$fetch">Refresh</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mountains: []
    }
  },
  async fetch() {
    this.mountains = await fetch(
      'https://api.nuxtjs.dev/mountains'
    ).then(res => res.json())
  }
}
</script>