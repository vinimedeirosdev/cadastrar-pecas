<template>
  <div class="main-container">
    <h1 class="title-banner">Peças Cadastradas</h1>
    <PecasCadastradas />
  </div>
</template>

<script>
import PecasCadastradas from "../components/PecasCadastradas.vue";
export default {
  name: "Pecas",
  components: {
    PecasCadastradas,
  },
};
</script>
