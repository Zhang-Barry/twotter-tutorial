<template>
  <div class="user-profile">
    <div class= "user-profile_user-panel">
      <h1 class="user-profile_username"> @{{user.username}}
          <img src="../assets/pfp.png"/>
      </h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile_follower-count">
          <strong>Followers: </strong> {{followers}}
      </div>
    </div>
      <div class ="user-profile_twoots-wrapper">
      <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot"/>
    </div>
  </div>

</template>

<script>

import TwootItem from "./TwootItem.vue";

export default {
  name: "UserProfile",
  components: {TwootItem}, 
  data(){
    return{
      followers: 69,
      user: {
        id: 1,
        username: '_Johnson Li',
        firstName: 'Johnson',
        lastName: 'Li',
        email: 'johnsonli@coolmail.com',
        isAdmin: true,
        twoots: [
          { id: 1, content: 'Twotter is Amazing!'},
          { id : 2, content: 'Cool website' }
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if (oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower! `)
      }
    }
  },
  computed: {
    fullName(){
      //return this.user.firstName + ' ' + this.user.lastName;
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods:{
    followUser(){
      this.followers++

    }
  },
  mounted(){
    this.followUser();
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  text-align: center;
} */


.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

img{
  width: 10%;
  height: auto;
  border-radius: 5px;
}

.user-profile_user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #1DA1F2;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    color: #F5F8FA;
}

.user-profile_admin-badge{
  background: purple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;

}
h1 {
    margin: 0;
}

</style>
