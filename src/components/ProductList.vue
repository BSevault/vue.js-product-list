<template>
    <h1>Liste des produits</h1>
    <div class="product-list">
            <ProductCard
                v-for="product of products"
                :key="product.id"
                :product="product"
            />

    </div>
</template>

<script>
import { ref } from "vue";
import ProductCard from './ProductCard.vue';

export default {
    name: 'ProductList',
    components: {
        ProductCard
    },
    data() {
        const products = ref(null);

        fetch("https://fakestoreapi.com/products")
            .then((res) => res.json())
            .then((json) => (products.value = json));
        return { products };
    }
}

</script>

<style scoped>
    .product-list {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }    
</style>
