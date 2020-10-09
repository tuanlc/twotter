<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">
          Twooter
        </div>
      </router-link>
      <div class="navigation__user">
        {{ state.user.username }}
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script>
import { reactive } from 'vue';

export default {
  name: 'App',
  setup() {
    const state = reactive({
      user: {
        username: '_TuanLECONG'
      }
    });

    return {
      state
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
}

nav {
  padding: 30px;
}
</style>
