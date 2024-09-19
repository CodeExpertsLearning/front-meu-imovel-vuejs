<script setup>
import { computed, onMounted, reactive, ref } from "vue";

// const url = ref("localhost.com");
const showClass = ref(false);
const imoveis = ref([]);
const imovel = reactive({ endereco: {} });

const totalImoveis = computed(() => `Total Imoveis: ${imoveis.value.length}`);

onMounted(() => {
  //mdn.io/fetch
  fetch("http://localhost:3030/imoveis")
    .then((resposta) => resposta.json())
    .then((data) => (imoveis.value = data));
});

const salvarImovel = () => {
  // console.log(imovel);
  fetch("http://localhost:3030/imoveis", {
    method: "POST",
    body: JSON.stringify(imovel),
    headers: { "Content-Type": "application/json" },
  })
    .then((response) => response.json())
    .then((data) => imoveis.value.push(data));
};

// const nome = ref("João");
// const curso = reactive({ uiid: "00-00-00-00", nome: "PHP Mastery" });
// const frutas = ["maçã", "pera", "abacaxi"];
// const mostrar = ref(false);

// const usuarios = [
//   { id: 1, nome: "Joao" },
//   { id: 2, nome: "Pedro" },
//   { id: 3, nome: "Marcos" },
// ];

const hello = () => {
  // nome.value = "Pedro";
  // console.log(nome.value);

  // curso.nome = "PHP API REST";
  // mostrar.value = !!!mostrar.value;

  showClass.value = !!!showClass.value;
};
</script>

<template>
  <div>
    <!-- <a :href="`http://${url}`">Link</a> -->
    <button @click="hello">Clique Aqui</button>

    <small :class="{ 'bg-black p-10': showClass }">{{ totalImoveis }}</small>
    <div>
      <input placeholder="cidade_id" v-model="imovel.cidade_id" type="text" />
      <input
        placeholder="imovel_area"
        v-model="imovel.imovel_area"
        type="text"
      />
      <input placeholder="estado_id" v-model="imovel.estado_id" type="text" />
      <input
        placeholder="total_imovel_area"
        v-model="imovel.total_imovel_area"
        type="text"
      />
      <input placeholder="titulo" v-model="imovel.titulo" type="text" />
      <input placeholder="banheiros" v-model="imovel.banheiros" type="text" />
      <input placeholder="descricao" v-model="imovel.descricao" type="text" />
      <input placeholder="quartos" v-model="imovel.quartos" type="text" />
      <input placeholder="conteudo" v-model="imovel.conteudo" type="text" />
      <input placeholder="price" v-model="imovel.price" type="text" />
      <input placeholder="slug" v-model="imovel.slug" type="text" />
      <input
        placeholder="endereco.endereco"
        v-model="imovel.endereco.endereco"
        type="text"
      />
      <input
        placeholder="endereco.bairro"
        v-model="imovel.endereco.bairro"
        type="text"
      />
      <input
        placeholder="endereco.numero"
        v-model="imovel.endereco.numero"
        type="text"
      />
      <input
        placeholder="endereco.cep"
        v-model="imovel.endereco.cep"
        type="text"
      />

      <button @click="salvarImovel">Salvar</button>
    </div>
    <hr />
    <h2>Imóveis</h2>
    <ul>
      <li v-for="imovel of imoveis" :key="imovel.id">
        {{ imovel.titulo }}
      </li>
    </ul>
    <!-- <p>
      {{ nome }} <br />
      <input type="text" v-model="nome" />

      <input type="hidden" v-model="curso.nome" />
    </p>
    <button @click="hello">Clique Aqui</button>

    <hr />

    Curso: {{ curso.nome }} / {{ curso.uiid }}

    <hr />

    <h2>Usuários</h2>
    <ul>
      <li v-for="usuario of usuarios" :key="usuario.id">
        {{ usuario.id }} - {{ usuario.nome }}
      </li>
    </ul>

    <ul>
      <li v-for="(fruta, index) of frutas" :key="index">
        {{ index }} - {{ fruta }}
      </li>
    </ul>

    <hr />

    <h2>Condicionais</h2>
    <p v-if="mostrar">Exibir conteúdo...</p>
    <small v-else>Padrao pro mostrar false...</small> -->
  </div>
</template>

<style scoped>
.p-10 {
  padding: 10px;
}
.bg-black {
  background-color: black;
}
</style>
