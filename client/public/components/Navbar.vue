<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <router-link
      to="/"
      class="navbar-brand">
      <img src="img/logopopo.png">
    </router-link>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarNavDropdown">
      <span class="navbar-toggler-icon" />
    </button>
    <div
      id="navbarNavDropdown"
      class="collapse navbar-collapse justify-content-end">
      <ul class="navbar-nav">
        <li class="nav-item">
          <router-link
            to="/"
            class="nav-link">Home
          </router-link>
        </li>
        <li
          v-if="user && user.role == 'driver'"
          class="nav-item">
          <router-link
            to="/myrides"
            class="nav-link">My Rides
          </router-link>
        </li>
        <li
          v-if="user && user.role == 'passenger'"
          class="nav-item">
          <router-link
            to="/mybids"
            class="nav-link">My Bids
          </router-link>
        </li>
        <li
          v-if="user"
          class="nav-item">
          <router-link
            to="/profile"
            class="nav-link">Profile
          </router-link>
        </li>
        <li
          v-if="user"
          class="nav-item">
          <a
            href="/api/logout"
            class="nav-link">Logout
          </a>
        </li>
        <li
          v-if="!user"
          class="nav-item">
          <router-link
            to="/login"
            class="nav-link">Login (Passenger)
          </router-link>
        </li>
        <li
          v-if="!user"
          class="nav-item">
          <router-link
            to="/login/driver"
            class="nav-link">Login (Driver)
          </router-link>
        </li>
        <li
          v-if="!user"
          class="nav-item">
          <router-link
            to="/register"
            class="nav-link">Register
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import 'bootstrap/dist/js/bootstrap.min.js';
export default {
  name: 'Navbar',
  props: {
    user: {
      type: Object,
      default: null,
      required: false
    }
  }
}
</script>

<style scoped>
  .navbar-brand img {
    height: 40px;
  }
</style>
