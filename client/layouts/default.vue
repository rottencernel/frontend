<template>
  <div>
    <Nav />
    <div class="container">
      <Nuxt />
    </div>
  </div>
</template>


<script>
import Nav from "~/components/Nav";

export default {
  components: {
    Nav,
  },

  head() {
    return {
      link: [
        { rel: "canonical", href: `http://localhost:3000${this.$route.path}`}
      ]
    }
  },
};

</script>

<style>

</style>