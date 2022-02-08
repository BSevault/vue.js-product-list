<template>
    <div class="product-card">
        <img :src="product.image" />
        <h2>{{ product.title }}</h2>
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
         }
};
</script>

<style scoped>
.product-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
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
