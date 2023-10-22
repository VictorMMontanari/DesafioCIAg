<script setup>
import { ref, computed, onMounted, reactive } from 'vue';
import ListProd from '../components/ListProd.vue';
import CarregarProd from '../components/CarregarProd.vue';

const selectedOption = ref('ALL...');
const produtos = reactive([]);
const searchTerm = ref('');
const produtosLoaded = ref(false); 

onMounted(async () => {
  try {
    fetch('https://fakestoreapi.com/products')
      .then(res => res.json())
      .then(res => {
        produtos.value = res;
        produtosLoaded.value = true;
      });
  } catch (error) {
    console.error('Erro na solicitação:', error);
  }
});

const filteredProdutos = computed(() => {
  const sortedProdutos = [...produtos.value];

  if (!searchTerm.value) {
    if (selectedOption.value.toLowerCase() === "maior") {
      sortedProdutos.sort((a, b) => b.price - a.price);
    }
    else if (selectedOption.value.toLowerCase() === "menor") {
      sortedProdutos.sort((a, b) => a.price - b.price);
    }
  }
  const searchTermLower = searchTerm.value.toLowerCase();
  return sortedProdutos.filter(produto => produto.title.toLowerCase().includes(searchTermLower));
});

</script>
<template>
  <main class="principal">
    <div class="container conteudo">
      <div class="conteudo2">
        <form class="row row-cols-lg-auto g-3 align-items-center">
          <div class="col-12">
            <input id="inline-form-input-name" class="form-control mb-2 mb-sm-0 mr-sm-2" placeholder="Nome do Produto"
              v-model="searchTerm" />
          </div>
          <div class="col-12">
            <label class="visually-hidden" for="inlineFormSelectPref">Preference</label>
            <select class="form-select" id="inlineFormSelectPref" v-model="selectedOption">
              <option selected>ALL...</option>
              <option value="maior">Maior</option>
              <option value="menor">Menor</option>
            </select>
          </div>
        </form>
      </div>
      <div class="row">
        <div class="col">
          <div class=" text-center conteudo2">
            <div class="card-body row g-3">
              <ListProd v-if="produtosLoaded" v-for="produto in filteredProdutos"
                :key="produto.id"
                :id="produto.id"
                :title="produto.title"
                :preco="produto.price"
                :descricao="produto.description"
                :categoria="produto.category"
                :img="produto.image"
                :avalicao="produto.rating.rate"
                :qtd="produto.rating.count"/>
              <CarregarProd v-else/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
.conteudo {
  position: relative;
  height: 100%;
  overflow-y: scroll;
  background-color: #fff;
  padding: 20px;
  box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.2);
  text-align: center;
  border-radius: 10px;
}

.principal {
  grid-area: principal;
  height: calc(100vh - 58px);
  background-color: #f0f0f0;
  padding: 20px;
}

.conteudo2 {
  position: relative;
  padding: 10px;
  box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.2);
  text-align: center;
  margin-bottom: 10px;
  border-radius: 10px;
}

::-webkit-scrollbar {
  width: 15px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: #888;
  height: 3rem;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: #1a1a1a;
}
</style>
