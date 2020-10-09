<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ state.user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="state.user.isAdmin">Admin</div>
      <div class="user-profile_admin-badge" v-else>Not Admin</div>
      <div class="user-profile_follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>

      <CreateTwootPanel @add-twoot="createNewTwoot"/>

    </div>
    <div class="user-profile_twoots-wrapper">
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
import { reactive, computed } from 'vue';
import { useRoute } from 'vue-router';

import users from '../assets/users';
import TwootItem from "../components/TwootItem";
import CreateTwootPanel from "../components/CreateTwootPanel";

export default {
  name: "UserProfile",
  components: {
    TwootItem,
    CreateTwootPanel
  },
  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId);

    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0]
    });

    const fullName = computed(() => `${state.user.firstName} ${state.user.lastName}`);

    function followUser() {
      state.followers++;
    }

    function createNewTwoot(newTwootContent) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: newTwootContent
      });
    }

    return {
      state,
      fullName,
      followUser,
      createNewTwoot,
      userId
    };
  }
};
</script>

<style lang='scss' scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    h1 {
      margin: 0;
    }

    .user-profile_admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }

  .user-profile_twoots-wrapper {
    display: grid;
    grid-gap: 10px;
  }
}
</style>