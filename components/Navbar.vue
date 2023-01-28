<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand to="/">My Car web</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse2"></b-navbar-toggle>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      
      <b-collapse id="nav-collapse2" is-nav>
        <b-navbar-nav class="ml-auto">
          <!-- <div class="collapse navbar-collapse" id="collapsibleNavId"> -->
            <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
              <li class="nav-item ">
                <a class="nav-link" href="/CarrosCompoent">Carros </a>
              </li>
              <li class="nav-item ">
                <a class="nav-link" href="/ClientePage">Clientes</a>
              </li>
              <li class="nav-item ">
                <a class="nav-link" href="/OrdemPage">Ordem de Compras</a>
              </li>
              <li class="nav-item ">
                <a class="nav-link" href="/FinanPage">Analytics</a>
              </li>
            </ul>
          <!-- </div> -->
        </b-navbar-nav>  
      </b-collapse>
     
      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto" v-if="isAuthenticated">
          <!-- <b-nav-item href="#">Link</b-nav-item> -->
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>{{ loggedInUser.name }}</em>
            </template>
            <li>
              <nuxt-link class="dropdown-item" to="/profile">Profile</nuxt-link>
            </li>
            <li>
              <a @click="logout" class="dropdown-item" href="#">Log out</a>
            </li>
          </b-nav-item-dropdown>
        </b-navbar-nav>

        <b-navbar-nav class="ml-auto" v-else>
          <li class="nav-item">
            <nuxt-link class="nav-link" to="/register">Register</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" to="/login">Log In</nuxt-link>
          </li>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
  import {
    mapGetters
  } from 'vuex'

  export default {
    name: "Navbar-d",
    computed: {
      ...mapGetters(['isAuthenticated', 'loggedInUser'])
    },
    methods: {
      async logout() {
        await this.$auth.logout();
      },
    },
  }

</script>

<style>

.side-lateral{
  background-color: rgb(56, 48, 48);
    height: 400px;
    width: 30%;
    z-index: 20;
    position: absolute;
    
}

</style>