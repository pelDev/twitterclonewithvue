<template>
  <div class="user-profile">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">
            @{{user.userName}}
        </h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">
            Admin
        </div>
        <div class="user-profile__follower-count">
            <strong>Followers: </strong> {{followers}}
        </div>
      </div>

      <div class="user-profile__tweets-wrapper">
          <TweetItem v-for="tweet in user.tweets" :key="tweet.id" :username='user.userName' :tweet='tweet'/>
      </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem";
export default {
    components: {
        TweetItem
    },
    name: 'User Profile',
    data() {
    return {
      followers: 0,
      user: {
        id: 1,
        userName: 'akinrelepelumi',
        firstName: 'Pelumi',
        lastName: 'Akinrele',
        email: 'pelumip15@gmail.com',
        isAdmin: true,
        tweets: [
            {id: 1, content: 'Twitter is Amazing!'},
            {id: 2, content: "Don't forget to subscribe to pelDev tutorials"}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if(oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.userName} just gained a follower!`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    }
  },
  mounted() {
    this.followUser();
  }

}
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    padding: 50px 5%;
}
.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 5px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid grey;
}

h1 {
    margin: 0;
}

.user-profile__follower-count {
    margin-top: 3px;
}

.user-profile__admin-badge {
    background: rebeccapurple;
    border-radius: 5px;
    margin-right: auto;
    color: white;
    padding: 0px 10px;
    margin-top: 3px;
    margin-bottom: 3px;
    font-weight: bold;
}
</style>












