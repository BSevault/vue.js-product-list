<template>
    <h1>Liste des produits</h1>
    <div class="product-list">
            <div
                v-for="product of products"
                :key="product.id"
                :id="'product-' + product.id"
            >
                <h2>{{ product.title }}</h2>
            </div>
    </div>
</template>

<script>
import { ref } from "vue";

export default {
    name: "ProductList",
    setup() {
        const products = ref(null);

        fetch("https://fakestoreapi.com/products")
            .then((res) => res.json())
            .then((json) => (products.value = json));
        console.log(products);
        return { products };
    },
};
</script>

<style scoped></style>
