<template>
  <section>
    <Navbar :logo="logo_src" :alt="logo_alt" />
    <router-view />
    <Footer />
  </section>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
export default {
  data() {
    return {
      logo_src: "/img/logo.png",
      logo_alt: "logo app",
    };
  },
  components: {
    Navbar,
    Footer,
  },
};
</script>

<style>
* {
  font-family: Arial, Helvetica, sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 50px;
  min-height: 250px;
}

h1 {
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
}

.title-banner {
  border-bottom: 4px solid #eac74d;
}
</style>
