<template>
  <div id="peca-table">
    <Msg :msg="msg" v-show="msg" />
    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Carro</th>
          <th>Valor</th>
          <th>Quantidade</th>
          <th>Código</th>
          <th>Ação</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="peca in pecas" :key="peca.id">
          <td>{{ peca.nome }}</td>
          <td>{{ peca.carro }}</td>
          <td>R$ {{ peca.valor }}</td>
          <td>{{ peca.quantidade }}</td>
          <td>{{ peca.cod }}</td>
          <td>
            <button class="edit">
              <router-link :to="{ path: '/edit/' + peca.id }" class="link"
                >Editar</router-link
              >
            </button>
            <button class="delete" @click="deletePeca(peca.id)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Msg from "./Msg.vue";

export default {
  name: "PecasCadastradas",
  data() {
    return {
      pecas: null,
      msg: null,
    };
  },
  components: {
    Msg,
  },
  methods: {
    async getPecas() {
      const req = await fetch("http://localhost:3000/items");

      const data = await req.json();

      this.pecas = data;
    },

    async deletePeca(id) {
      const req = await fetch(`http://localhost:3000/items/${id}`, {
        method: "DELETE",
      });

      const res = await req.json();

      this.msg = "Peça Deletada!";

      setTimeout(() => (this.msg = ""), 5000);

      this.getPecas();
    },
  },
  mounted() {
    this.getPecas();
  },
};
</script>

<style scoped>
table {
  width: 100%;
}

th,
td {
  padding: 12px 15px;
  text-align: left;
  border-bottom: 1px solid #dddddd;
}

th {
  background-color: #91d3ed;
  font-weight: bold;
}

tr:hover {
  background-color: #f5f5f5;
}

.edit {
  background-color: #0b73d3;
}

.link {
  text-decoration: none;
  color: #fff;
}

.delete {
  background-color: #f44336;
}
.edit,
.delete {
  color: white;
  padding: 6px 10px;
  margin: 3px;
  border: none;
  cursor: pointer;
  font-size: 14px;
}

.edit:hover {
  background-color: #064987;
}

.delete:hover {
  background-color: #c9302c;
}
</style>
