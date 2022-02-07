<template>
    <h1>Liste des produits</h1>
    <div class="product-list">
            <div class="product-card"
                v-for="product of products"
                :key="product.id"
            >
            <h2> {{product.title}} </h2>
            <img :src="product.image">
            <p> {{product.description}} </p>
            <p><strong> {{product.price}} € </strong></p>
            <p> Rating : {{product.rating.rate}} &#9733; / {{product.rating.count}} </p>

            </div>

    </div>
</template>

<script>
import { ref } from "vue";

export default {
    name: "ProductList",
    data() {
        const products = ref(null);

        fetch("https://fakestoreapi.com/products")
            .then((res) => res.json())
            .then((json) => (products.value = json));
        console.log(products);
        return { products };
    }




};
</script>

<style scoped>
    .product-card img {
        max-width: 120px;;
    }
</style>
