<script setup>
const props = defineProps(["id", "title", "preco", "descricao", "categoria", "img", "avalicao", "qtd"])
</script>

<template>
    <div>
        <div class="image-container">
            <img :src="img" decoding="async" class="card-img" alt="..." />
        </div>
    </div>
</template>