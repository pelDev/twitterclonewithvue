<template>
    <div class="tweet-item" @click="favouriteTweet(tweet.id)">
        <div class="user-profile__tweet">
            <div class="tweet-item__user">
                @{{username}}
            </div>
            <div class="teet-item__content">
                {{tweet.content}}
            </div>
        </div>
    </div>    
</template>

<script>
export default {
    name: 'TweetItem',
    props: {
        username: {
            type: String,
            required: true
        }, 
        
        tweet: {
            type: Object,
            required: true
        }

    
    },
    methods: {
        favouriteTweet(id) {
            this.$emit('favourite', id);
        }
    }
}
</script>

<style lang="scss" scoped>
.tweet-item {
    padding: 20px;
    cursor: pointer;
    background-color: white;
    border: 1px solid #dfe3e8;
    box-sizing: border-box;
    transition: all 0.25 ease;
    border-radius: 5px;

    &:hover { 
        transform: scale(1.1, 1.1);
    }
    
    .tweet-item__user {
        font-weight: bold;   
    }
}



</style>