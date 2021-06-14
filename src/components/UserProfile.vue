<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ state.user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>
      <CreateTwootPanel @addtwoot="createNewTwoot" />
    </div>
    <div class="user-profile__twoots-wrapper">
        <TwootItem
            v-for="twoot in state.user.twoots" 
            :key="twoot.id"
            :username="state.user.username"
            :twoot="twoot"
        />
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue';
import TwootItem from './TwootItem';
import CreateTwootPanel from './CreateTwootPanel';

export default {
  name: 'UserProfile',
  components: { TwootItem, CreateTwootPanel },
  setup() {
    const state = reactive({
      followers: 0,
      user: {
        id: 1,
        username: '_jsanchez',
        firstName: 'Jonathan',
        lastName: 'Sanchez',
        email: 'jsanchez.dev1991@gmail.com',
        isAdmin: true,
        twoots: [
            {
                id:1, content: 'Twotter is Amazing!'
            },
            {
                id:2, content: 'Dont forget to suscriber'
            }
        ]
      }
    });

    function createNewTwoot(newTwootContent) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: newTwootContent
      });
    }

    return {
      state,
      createNewTwoot
    }
  },

  mounted() {
    this.followUser();
  }
}
</script>


<style scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-gap: 50px;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
    margin-bottom: 20px;
}

h1 {
    margin: 0;
}

.user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
}

.user-profile__create-twoot {
    border-top: 1px solid #DFE3E8;
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}

.--exceeded {
  color:red;
  border-color: red;
}

.--exceeded button {
  background-color: red;
  border: none;
  color: white;
}
</style>
