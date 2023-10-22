<script setup>
import StarRating from './StarRating.vue';
const props = defineProps(["id", "title", "preco", "descricao", "categoria", "img", "avalicao", "qtd"])


</script>

<template>
    <div>
        <div class="image-container">
            <img :src="img" decoding="async" class="card-img" alt="..." />
        </div>
        <div>
            <div class="d-flex justify-content-center align-items-center">
                <StarRating v-model="selectedRating" :max="5" :avalicao="avalicao" />
            </div>
            <p>Nota: {{ avalicao }}</p>
            <h5>Categoria: </h5>
            <p>{{ categoria }}</p>
            <h5> Descrição </h5>
            <p>{{ descricao }}</p>
            <span>
                <h4>R$ {{ preco.toFixed(2) }}</h4>
            </span>
        </div>
    </div>
</template>