<script setup>
import { ref } from 'vue';
import StarRating from './StarRating.vue';
import InfoModal from './InfoModal.vue';

const selectedRating = ref(3);

const props = defineProps(["id", "title", "preco", "descricao", "categoria", "img", "avalicao", "qtd"])

const truncate = (text, length) => {
    if (text.length > length) {
        return text.substring(0, length) + '...';
    }
    return text;
};
</script>

<template>
    
    <div class="col-12 col-sm-4 col-md-3 col-lg-3">
        <a class="link" :data-bs-target="`#exampleModal-${id}`" data-bs-toggle="modal">
            <div class="card mb-3 hover">
                <div class="image-container">
                    <img :src="img" decoding="async" class="card-img" alt="..." />
                </div>
                <h5 class="th4">{{ truncate(title, 30) }}</h5>
                <div class="card-body text-center">
                    <div>
                        <div class="d-flex justify-content-center align-items-center">
                            <StarRating v-model="selectedRating" :max="5" :avalicao="avalicao" />
                        </div>
                        <p>Nota: {{ avalicao }}</p>
                        <h6 class="modal-title fs-5" id="exampleModalLabel">Categoria: </h6>
                        <p class="fs-6" id="exampleModalLabel">{{ categoria }}</p>
                        <span>
                            R$ {{ preco.toFixed(2) }}
                        </span>
                    </div>
                </div>
            </div>
        </a>
        <!-- Modal -->
        <div class="modal fade" :id="`exampleModal-${id}`" tabindex="-1" aria-labelledby="exampleModalLabel"
            aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">{{ title }}</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <InfoModal :id="id" :preco="preco" :descricao="descricao" :categoria="categoria" :img="img"
                            :avalicao="avalicao" :qtd="qtd" />
                    </div>
                    <div class="modal-footer">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
.link {
    display: inline;
    text-decoration: none;
    cursor: pointer;
}

.hover:hover {
    box-shadow: 0 0 6px 5px #ddd;
    border-radius: 6px;
    border: 1px solid #dee2e6;
}

.th4 {
    margin: 0px;
    color: #000000;
    padding: 10px 2rem 0px 2rem;
    font-weight: 400;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.card-img {
    max-width: 150px;
    max-height: 150px;
    padding: 16px 0px 16px 0px;
    width: auto;
    height: auto;
}

.image-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 150px;
    overflow: hidden;
    border-bottom: 1px solid rgba(0, 0, 0, 0.164);
}</style>