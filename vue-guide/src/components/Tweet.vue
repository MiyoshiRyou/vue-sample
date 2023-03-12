<script setup lang="ts">
import { ref } from 'vue'
import TweetPostForm from './TweetPostForm.vue'
import TweetList from './TweetList.vue'
const tweets = ref([{ id: 0, description: 'Hello, world!' }, { id: 1, description: 'this is the second tweet' }])
// const inputtingDescription = ref<string>('')

const postTweet = (description: string) => {
  const tweet = { id: Math.random(), description }
  tweets.value.push(tweet)
  // inputtingDescription.value = ''
  // console.log('inputting...', inputtingDescription.value)
  // console.log('post...', tweets.value)
}

const deleteTweet = (id: number) => {
  tweets.value = tweets.value.filter(t => t.id !== id)
}

</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <TweetPostForm @post-tweet="postTweet" />
    <!-- <input v-model="inputtingDescription" />
                          <button class="save-button" @click="postTweet()">post</button> -->
    <div class="tweet-container">
      <p v-if="tweets.length <= 0">No tweets have been added</p>
      <ul v-else>
        <TweetList :tweets="tweets" @delete-tweet="deleteTweet" />
        <!-- <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
                            <span>{{ tweet.description }}</span>
                            <button @click="deleteTweet(tweet.id)" class="delete-button">delete</button>
                          </li> -->
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  margin-bottom: 16px;
}

label {
  font-size: 20px;
  font-weight: bold;
}
</style>
