<template>
  <div class="column is-4 is-offset-4 my-auto">
    <div class="hero">
      <div class="hero-body">
        <div class="has-text-centered">
          <span class="is-inline-flex">
            <img class="image is-48x48" src="../assets/logo.png" />
            <h1 class="ml-3 title is-2">VacChain</h1>
          </span>
        </div>
        <form class="box my-5 p-5">
          <div class="field">
            <!-- <label class="label">Username</label> -->
            <p class="control has-icons-left has-icons-right">
              <input
                v-model="username"
                class="input"
                type="text"
                placeholder="Username"
              />
              <span class="icon is-small is-left">
                <FontAwesomeIcon icon="user" />
              </span>
            </p>
          </div>

          <div class="field">
            <!-- <label class="label">Password</label> -->
            <p class="control has-icons-left">
              <input
                v-model="password"
                class="input"
                type="password"
                placeholder="Password"
              />
              <span class="icon is-small is-left">
                <FontAwesomeIcon icon="lock" />
              </span>
            </p>
          </div>

          <div class="field">
            <p class="control">
              <button class="button is-primary is-fullwidth" @click="login">
                Login
              </button>
            </p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      username: '',
      password: '',
      isComplete: false,
      valid: false
    };
  },
  methods: {
    login() {
      //   this.$router.push('/admin');
      if (this.username === 'admin' && this.password === 'admin') {
        this.$router.push('/admin');
      }
    }
  }
};
</script>

<style scoped>
</style>