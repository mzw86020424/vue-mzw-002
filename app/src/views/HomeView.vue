<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
    <div v-for="tweet in tweets" :key="tweet.id">
      <Tweet :item="tweet"></Tweet>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from '../components/HelloWorld.vue';
import Tweet from '../components/Tweet.vue';
import Http from '../http-common'

export default defineComponent({
  name: 'HomeView',
  components: {
    HelloWorld,
    Tweet,
  },

  data() {
    return {
      tweets: JSON
    }
  },
  methods: {
    async fetchTweets():Promise<any> {
      let response = await Http.get(`/api/v1/tweets`);
      return response.data.data
    }
  },

  async mounted() {
    this.tweets = await this.fetchTweets()
  },
});
</script>
