<template>
  <div>
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

    <!-- show tweets -->
    <div class="col-md-12 col-sm-12">
      <div class="text-h6 text-weight-bold text-center">Tweets</div>
      <div
        v-for="(tweet, index) in tweets"
        :key="index"
        class="q-mb-md row justify-center full-width"
      >
        <q-card
          class="my-card q-mt-md shadow-3"
          v-if="tweets.length > 0"
          bordered
          dense
        >
          <q-card-section>
            <div class="text-body1">{{ tweet.text }}</div>
          </q-card-section>
          <q-card-actions>
            <q-btn flat  icon="mdi-calendar" />
            <q-btn flat> {{ tweet.date }} </q-btn>
            <q-btn flat icon="mdi-trash-can-outline" @click="removeTweet(index)" />
          </q-card-actions>
        </q-card>
        <div
          v-else
          class="text-negative text-weight-bold text-center text-body1"
        >
          No tweets to show, start tweeting :)
        </div>
      </div>
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
      // console.log(this.tweets);

      // transform object into string
      const stringTweets = JSON.stringify(this.tweets);
      console.log(stringTweets);
      //   add to local storage the stringify tweets
      localStorage.setItem("simple_tweet_tweets", stringTweets);
      //   localStorage.setItem("simple_tweet_tweets", JSON.stringify(this.tweets));

      // console.log("tweet submitted");
    },
    removeTweet(index){
let removeIt =  confirm('Are you sure you want to remove this tweet?')
if (removeIt){
  this.tweets.splice(index,1)
  // remove from local storage
  localStorage.simple_tweets_tweet = JSON.stringify(this.tweets)
}
    }
  }
};
</script>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 300px
</style>
