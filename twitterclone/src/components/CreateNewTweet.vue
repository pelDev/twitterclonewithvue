<template>
    <form class="user-profile__create-tweet" @submit.prevent="createNewTweet" :class="{'extended': newTweetCharacterCount > 180}">
          <label for="newTweet"><strong>New Tweet</strong> ({{ newTweetCharacterCount }}/180)</label>
          <textarea id="newTweet"  rows="4" v-model="newTweetContent"></textarea>
        
          <div class="user-profile__create-tweet-type">
            <label for="newTweetType"><strong>Type: </strong></label>
            <select id="newTweetType" v-model="selectedTweetType">
              <option 
              v-for="(option, index) in tweetTypes" 
              :value="option.value" 
              :key="index">
              {{option.name}}
              </option>
            </select>  
          </div>

          <button>
            Tweet
          </button>
        </form>
</template>

<script>

export default {
    name: "CreateNewTweet",
    data() {
        return {
            newTweetContent: 'dvd',
            selectedTweetType: 'instant',
            tweetTypes: [
                {value: 'draft', name: 'Draft'},
                {value: 'instant', name: 'Instant Tweet'}
            ],
        }
    },
    methods: {

        createNewTweet() {
            if(this.newTweetContent != '' && this.selectedTweetType != 'draft' && this.newTweetContent.length <= 180) {
                this.$emit('add-tweet', this.newTweetContent);
                console.log('Before emit ' + this.newTweetContent);
                this.newTweetContent = '';
            }
        }
        // createNewTweet() {
        //     if(this.newTweetContent != '' && this.selectedTweetType != 'draft' && this.newTweetContent.length <= 180) {
        //         this.user.tweets.unshift( {
        //         id: this.user.tweets.length + 1,
        //         content: this.newTweetContent,
        //         }) 
        //         this.newTweetContent = '';
        //     }
        // }
    },
    computed: {
        newTweetCharacterCount() {
            return this.newTweetContent.length;
        }
    },
}
</script>

<style lang="scss" scoped>
    .user-profile__create-tweet {
      padding-top: 20px;
      display: flex;
      flex-direction: column;

      &.extended {
        color: red;
        border-color: red;

        button {
          background-color: red;
          border: none;
          color: white;
        }
      }
    }
</style>