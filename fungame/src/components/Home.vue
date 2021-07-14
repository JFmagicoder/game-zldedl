<template>
  <div>
    <Header />
    <Footer />
  </div>
</template>

<script>
import Header from "./Header.vue";
import Footer from "./Footer";
export default {
  name: "Home",

  components: {
    Header,
    Footer,
  },

  data() {
    return {
    };
  },
};
</script>