<template>
  <div id="wrapper">
    <div
      id="particles-js"
      class="bg-primary"/>
    <div class="h-100 row d-flex align-items-center justify-content-center">
      <div class="col-sm-3">
        <h3 v-if="forDriver">Driver Login</h3>
        <h3 v-else>Passenger Login</h3>
        <form
          id="form"
          @submit.prevent="submitForm">
          <div class="form-group">
            <input
              v-model="formData.email"
              class="form-control"
              type="email"
              placeholder="email">
          </div>
          <div class="form-group">
            <input
              v-model="formData.password"
              class="form-control"
              type="password"
              placeholder="password">
          </div>
          <button
            type="submit"
            class="btn btn-submit">Login
          </button>
        </form>
        <router-link
          v-if="forDriver"
          to="/register/driver">Don't have an account?</router-link>
        <router-link
          v-else
          to="/register">Don't have an account?</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import './particles.min.js';
export default {
  props: {
    forDriver: {
      type: Boolean,
      default: false,
      required: false
    }
  },
  data() {
    return {
      formData: {
        email: '',
        password: ''
      }
    }
  },
  created () {
    if (this.$parent.user) {
      this.$router.push('/'); // if alr logged in, redirect away
    } else {
      /* eslint-disable no-undef */
      particlesJS.load('particles-js', '/particles.json');
    }
  },
  methods: {
    submitForm () {
      let url = this.forDriver ? 'api/login/driver' : 'api/login/passenger';
      fetch(url, {
        method: 'POST',
        body: JSON.stringify(this.formData),
        headers: {
          'content-type': 'application/json'
        },
        credentials: 'same-origin'
      })
      .then(res => {
        if (res.redirected) {
          if (!res.url.includes('login')) {
            window.location.href = '/';
          } else {
            this.$toasted.show('login failed');
          }
        }
      })
      .catch(this.$toasted.show);
    }
  }
}
</script>

<style scoped>
  #particles-js {
    height: 100%;
    width: 100%;
    position: fixed;
  }
  #wrapper {
    height: 100vh;
  }
  h3 {
    color: white;
  }
  a, a:hover {
    color: white;
  }
</style>
