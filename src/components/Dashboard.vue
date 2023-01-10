<template>
  <div id="burguer-table">

    <!-- Mensagem do sistema -->
    <Mensagem  :msg="msg" v-show="msg"/>

    <div>
      <div id="burguer-table-header">
        <div class="order-id">#</div>
          <div>Cliente:</div>
          <div>Pão:</div>
          <div>Carne:</div>
          <div>Opcionais:</div>
          <div>Ações:</div>
      </div>
    </div>
    <div id="burguer-table-rows">
      <div class="burguer-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number"> {{ burger.id }} </div>
        <div> {{ burger.nome }} </div>
        <div> {{ burger.pao }} </div>
        <div> {{ burger.carne }} </div>
        <div>
          <ul>
            <li v-for="(opcional, index) in burger.opcionais" :key="index">
              {{ opcional }}
            </li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updateBurger($event, burger.id)">
            <option value="">Selecione</option>
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo"> {{ s.tipo }} </option>
          </select>
          <button class="delete-btn" @click="deleteBurguer(burger.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Mensagem from "./Mensagem.vue"

export default {
  name: "Dashboard",
  components: {
    Mensagem
  },
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null
    }
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");

      const data = await req.json();

      this.burgers = data;

      //resgtando os status do backend
      this.getStatus();

    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");

      const data = await req.json();

      this.status = data
    },
    async deleteBurguer(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`,{
        method: "DELETE"
      });

      const res = req.json();

      //Inserindo mensagem de envio de pedido
      this.msg = `Pedido REMOVIDO com sucesso`
      
      //limpando mensagem da tela
      setTimeout(() => this.msg = "", 3000)

      this.getPedidos();

    },
    async updateBurger(event, id) {
      const option = event.target.value;
      
      const dataJson = JSON.stringify({ status: option })
      
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-type": "application/json"},
        body: dataJson
      })

      const res = await req.json();

      //Inserindo mensagem de atualização de pedido
      this.msg = `Pedido Nº ${res.id} foi atualizado para ${res.status}`
      
      //limpando mensagem da tela
      setTimeout(() => this.msg = "", 3000)

      console.log(res)
    }
  },
  mounted() {
    this.getPedidos();
  }
}
</script>

<style scoped>

#burguer-table {
  max-width: 1200px;
  margin: 0 auto;
}

#burguer-table-header,
#burguer-table-rows,
.burguer-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burguer-table-header {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}
.burguer-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #CCC;
}

#burguer-table-header div,
.burguer-table-row div {
  width: 19%; 
}

#burguer-table-header .order-id,
.burguer-table-row .order.number {
  width: 19%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}

.delete-btn {
  background-color: #222;
  color: #FCBA03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: .5s;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}

</style>
