<template>
  <div id="app">
    <input type="text" v-model="username" @change="handleChange">
    <div class="user" v-if="user.pending">
      Loading...
    </div>
    <div class="user" v-if="user.fulfilled">
      <img :src="user.value.avatar_url" width="80" :alt="user.value.login">
      <h2>{{ user.value.login }}</h2>
      <h3>{{ user.value.name }}</h3>
    </div>
    <div class="user" v-if="user.rejected">
      {{ user.reason.message }}
    </div>
  </div>
</template>

<script>
  import {mapState} from 'vuex'

  export default {
    name: 'app',
    data() {
      return {
        username: 'egoist'
      }
    },
    computed: {
      ...mapState(['user'])
    },
    fetch: {
      user() {
        return {
          url: `https://api.github.com/users/${this.username}`,
          commit: 'UPDATE_USER'
        }
      }
    },
    methods: {
      handleChange() {
        this.$fetch('user')
      }
    }
  }
</script>
