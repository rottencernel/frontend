<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light sticky-top">
 
    <button class="navbar-toggler" type="button" data-toggle="collapse"
            data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <nuxt-link class="nav-link" to="/">Главная</nuxt-link>
        </li>
        <li class="nav-item active">
          <nuxt-link class="nav-link" to="/about">Пару слов об этом блоге</nuxt-link>
        </li>
      </ul>
       <span class="navbar-text mr-2" v-if="user">{{user.username}}</span>
     <client-only>
      <span v-if="loggedIn"><nuxt-link class="btn btn-outline-lwarning text-dark mr-2" to="/signout">Выход</nuxt-link></span>
      <span v-else>
        <nuxt-link class="btn btn-outline-warning text-dark mr-2" to="/signin">Вход</nuxt-link>
        <nuxt-link class="btn btn-outline-warning text-dark mr-2" to="/signup">Регистрация</nuxt-link>
      </span>
    </client-only>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  data(){
    return {
      q : null
    }
  },
  methods: {
    submit(){
      this.$router.push("/search?q="+this.q);
    }
  },

  computed: {
    loggedIn() {
      return this.$auth.loggedIn
    },
    user() {
      return this.$auth.user
    }
  }
}
</script>

<style scoped>

</style>