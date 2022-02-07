<template>
    <div class="product-card">
        <h2>{{ product.title }}</h2>
        <img :src="product.image" />
        <p>{{ product.description }}</p>
        <p>
            <strong> {{ product.price }} € </strong>
        </p>
        <p class="category"> {{product.category}} </p>
        <p>
            Rating : {{ product.rating.rate }} &#9733; /
            {{ product.rating.count }}
        </p>

    </div>
</template>

<script>
export default {
    name: 'ProductCard',
    props: {
         product: Object 
         },
};
</script>

<style scoped>
.product-card {
    width: 400px;
    margin: 15px;
    border: 1px solid black;
}

.product-card img {
    max-width: 120px;
}

.product-card .category {
    text-transform: capitalize;
}
</style>
