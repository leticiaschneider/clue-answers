<script setup lang="ts">
import CustomButton from './components/CustomButton.vue';
import { reactive, ref } from 'vue';

const buttonText = 'Texto ddddDinâmico';
const icon = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"/></svg>';

let quemList: any = ref([
  { value: 'Green', resposta: '' },
  { value: 'Mostarda', resposta: '' },
  { value: 'Peacock', resposta: '' },
  { value: 'Plum', resposta: '' },
  { value: 'Scarlet', resposta: '' },
  { value: 'White', resposta: '' }
]);

let oQueList: any = ref([
  { value: 'Chave Inglesa', resposta: '' },
  { value: 'Castiçal', resposta: '' },
  { value: 'Faca', resposta: '' },
  { value: 'Revolver', resposta: '' },
  { value: 'Cano de chumbo', resposta: '' },
  { value: 'Corda', resposta: '' }
]);

const state = reactive({
  mansaoList: [
    { value: 'Banheiro', resposta: '' },
    { value: 'Escritorio', resposta: '' },
    { value: 'Sala de Jantar', resposta: '' },
    { value: 'Sala de Jogos', resposta: '' },
    { value: 'Garagem', resposta: '' },
    { value: 'Quarto', resposta: '' },
    { value: 'Sala de Estar', resposta: '' },
    { value: 'Cozinha', resposta: '' },
    { value: 'Entrada', resposta: '' }
  ],
  praiaList: [
    { value: 'Praia', resposta: '' },
    { value: 'Fliperama', resposta: '' },
    { value: 'Aluguel de Jet Ski', resposta: '' },
    { value: 'P. de Diversões', resposta: '' },
    { value: 'Loja de Surfe', resposta: '' },
    { value: 'Casa de Praia', resposta: '' }
  ],
  listOndeChoose: ref<any[]>([]),
});

state.listOndeChoose = [...state.mansaoList];

const estados = ref(['X', '✔️', '?']);

const alterarEstado = (item: any) => {
  item.resposta = estados.value[(estados.value.indexOf(item.resposta) + 1) % estados.value.length];
};

const respostaFormatada = (resposta: string) => {
  if (resposta === 'X') return 'X';
  if (resposta === '✔️') return '✔️';
  if (resposta === '?') return '?';
  return '';
};

const handleButtonClick = (value: string) => {
  state.praiaList = state.praiaList.map(item => ({ ...item, resposta: '' }));
  state.mansaoList = state.mansaoList.map(item => ({ ...item, resposta: '' }));

  state.listOndeChoose = value === 'Praia' ? [...state.praiaList] : [...state.mansaoList];
};

const limparCampos = () => {
  // quemList = quemList.map((item: any) => ({ ...item, resposta: '' }));
  // oQueList = oQueList.map((item: any) => ({ ...item, resposta: '' }));

  for (let i = 0; i < quemList.value.length; i++) {
    quemList.value[i].resposta = '';
  }

  for (let i = 0; i < oQueList.value.length; i++) {
    oQueList.value[i].resposta = '';
  }

  state.praiaList.forEach(item => {
    item.resposta = '';
  });

  state.mansaoList.forEach(item => {
    item.resposta = '';
  });

  state.listOndeChoose.forEach(item => {
    item.resposta = '';
  });

  // state.praiaList.map(item => ({ ...item, resposta: '' }));
  // state.mansaoList.map(item => ({ ...item, resposta: '' }));
};

</script>

<template>
  <header>
    <custom-button @buttonClick="handleButtonClick" buttonText="Mansão" />
    <custom-button @buttonClick="handleButtonClick" buttonText="Praia" />
  </header>

  <main>
    <table>
      <tr>
        <th colspan="2">QUEM?</th>
      </tr>
      <tr v-for="(quem, index) in quemList" :key="index">
        <td>{{ quem.value }}</td>
        <th :class="'color-' + (quem.resposta === '?' ? 'dubbio' : quem.resposta)" @click="alterarEstado(quem)">{{
          respostaFormatada(quem.resposta) }}</th>
      </tr>
      <tr>
        <th colspan="2">O QUÊ?</th>
      </tr>
      <tr v-for="(oQue, index) in oQueList" :key="index">
        <td>{{ oQue.value }}</td>
        <th :class="'color-' + (oQue.resposta === '?' ? 'dubbio' : oQue.resposta)" @click="alterarEstado(oQue)">{{
          oQue.resposta }}</th>
      </tr>
      <tr>
        <th colspan="2">ONDE?</th>
      </tr>
      <tr v-for="(onde, index) in state.listOndeChoose" :key="index">
        <td>{{ onde.value }}</td>
        <th :class="'color-' + (onde.resposta === '?' ? 'dubbio' : onde.resposta)" @click="alterarEstado(onde)">{{
          onde.resposta }}</th>
      </tr>
    </table>
  </main>

  <footer>
    <custom-button @buttonClick="limparCampos" buttonText="Limpar Campos" />
  </footer>
</template>

<style scoped>
header {
  text-align: center;
  margin: 20px 0;
}

table {
  border-collapse: collapse;
  width: 90%;
  margin: 0 auto;
  margin-bottom: 90px;
}

th,
td {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
  width: 50px;
  height: 50px;
  text-align: center;
}

.color-X {
  background-color: rgb(200, 113, 113);
}

.color-✔️ {
  background-color: rgb(94, 208, 149);
}

.color-dubbio {
  background-color: rgb(179, 139, 240);
}

footer {
  text-align: center;
  margin-bottom: 50px;
}
</style>
