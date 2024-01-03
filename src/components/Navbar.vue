<template>
  <div id="nav">
    <router-link to="/" id="logo_banner"><img :src="logo" :alt="alt" id="logo" /></router-link>
    <router-link to="/">Cadastrar</router-link> |
    <router-link to="/pecas">Peças Cadastradas</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
#nav {
  background-color: #143985;
  border-bottom: 4px solid #eac74d;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;

}

#logo {
  width: 85px;
  height: 85px;
  border-radius: 50px;
}

#nav #logo_banner {
    margin: auto;
    margin-left: 0;
}

#nav a {
    color: #FFF;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
}

#nav a:hover {
    color: #eac74d;
}
</style>
