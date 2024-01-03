<template>
  <div class="main-container">
    <h1 class="title-banner">Cadastro de Peça</h1>
    <PecaFormulario />
  </div>
</template>

<script>
import PecaFormulario from "../components/PecaFormulario.vue";

export default {
  name: "Home",
  components: {
    PecaFormulario
  },
};
</script>

<style scoped>

</style>
