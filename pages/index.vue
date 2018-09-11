<template>
  <div>
    <Header :image="headerImage"/>
    <section class="container">
      <div></div>
    </section>
  </div>
</template>

<script>
import Header from "~/components/Header";

export default {
  async asyncData({ app, store, params }) {
    if (!store.state.page) {
      let page = await app.$axios.get(
        `${store.state.wordpressAPI}/wp/v2/pages/12?_embed`
      );

      store.commit("setPage", page.data);
    }
  },

  components: {
    Header
  },

  computed: {
    headerImage() {
      return this.$store.state.page._embedded["wp:featuredmedia"][0].source_url;
    }
  }
};
</script>

<style scoped>
.header {
  height: 400px;
}
</style>

