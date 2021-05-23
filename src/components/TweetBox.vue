<template>
  <div class="row  justify-center">
    <div class="q-pa-md " style="width: 400px">
      <q-form @submit.prevent="sendTweet" class="q-ma-md">
        <label for="tweet" class="text-weight-bold text-grey q-ma-md"
          >Send your tweet</label
        >
        <q-input
          v-model="tweetMsg"
          outlined
          rounded
          autogrow
          counter
          maxlength="200"
        />
        <div>
          <q-btn
            label="Tweet"
            no-caps
            type="submit"
            color="primary"
            rounded
            class="full-width q-mt-md"
          />
        </div>
      </q-form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tweetMsg: "", //current tweet
      tweets: [] //lists of tweets array
    };
  },
  methods: {
    sendTweet() {
      // store tweets in tweets array
      this.tweets.unshift({
        text: this.tweetMsg,
        date: new Date().toLocaleTimeString()
      });
      // empty tweet property and clear the textarea field
      this.tweetMsg = "";
      console.log(this.tweets);

      // transform object into string
      const stringTweets = JSON.stringify(this.tweets);
      console.log(stringTweets);
      //   add to local storage the stringify tweets
      localStorage.setItem("simple_tweet_tweets", stringTweets);
      //   localStorage.setItem("simple_tweet_tweets", JSON.stringify(this.tweets));

      console.log("tweet submitted");
    }
  }
};
</script>
