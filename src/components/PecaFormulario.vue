<template>
  <div>
    <Msg :msg="msg" v-show="msg" />
    <div>
      <form id="peca-form" @submit="createPeca">
        <div class="input_container">
          <label for="nome">Nome:</label>
          <input type="text" id="nome" name="nome" v-model="nome" required />
        </div>
        <div class="input_container">
          <label for="carro">Carro:</label>
          <input
            list="carros"
            id="carro"
            name="carro"
            v-model="carro"
            required
          />
          <datalist id="carros" required>
            <option
              v-for="carro in carros"
              :key="carro.id"
              :value="carro.model"
            >
              {{ carro.model }}
            </option>
          </datalist>
        </div>
        <div class="input_container">
          <label for="valor">Valor:</label>
          <input type="text" id="valor" name="valor" v-model="valor" required />
        </div>
        <div class="input_container">
          <label for="quantidade">Quantidade:</label>
          <input
            type="number"
            id="quantidade"
            name="quantidade"
            v-model="quantidade"
            required
          />
        </div>
        <div class="input_container">
          <label for="cod">Código:</label>
          <input type="text" id="cod" name="cod" v-model="cod" required />
        </div>
        <div class="input_container">
          <input type="submit" class="submit_btn" value="Cadastrar Peça" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Msg from "./Msg.vue";

export default {
  components: {
    Msg,
  },
  name: "PecaFormulario",
  data() {
    return {
      nome: null,
      carro: null,
      carros: null,
      valor: null,
      quantidade: null,
      cod: null,
      msg: null,
    };
  },
  methods: {
    async getModelos() {
      const req = await fetch("http://localhost:3000/pecas_cadastradas");
      const data = await req.json();

      this.carros = data.modelos;
    },
    async createPeca(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        carro: this.carro,
        valor: parseFloat(this.valor),
        quantidade: this.quantidade,
        cod: this.cod.toUpperCase(),
      };
      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/items", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      this.msg = "Peça cadastrata com sucesso!";

      setTimeout(() => (this.msg = ""), 5000);

      this.nome = "";
      this.carro = "";
      this.valor = "";
      this.quantidade = "";
      this.cod = "";
    },
  },
  mounted() {
    this.getModelos();
  },
};
</script>

<style scoped>
#peca-form {
  max-width: 400px;
  margin: 0 auto;
  border: 2px solid;
  padding: 10px;
  box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
}
.input_container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  padding: 5px 10px;
}

input {
  padding: 5px 10px;
  width: 300px;
}

.submit_btn {
  background-color: #eac74d;
  font-weight: bold;
  transition: 0.5s;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
}

.submit_btn:hover {
  color: #fff;
}
</style>
