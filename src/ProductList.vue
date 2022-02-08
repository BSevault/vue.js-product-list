<template>
    <h1>Our products</h1>
    <sorting-select 
        @sortingOption="sortingMode($event)"
    ></sorting-select>
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
import ProductCard from "./components/ProductCard.vue";
import SortingSelect from "./components/SortingSelect.vue";

export default {
    name: "ProductList",
    components: {
        ProductCard,
        SortingSelect
        
    },

    data() {
        // Getting the product list as a json with fetch(), and pass it to ProductCard component as props
        const products = ref(null);

        fetch("https://fakestoreapi.com/products")
            .then((res) => res.json())
            .then((json) => (products.value = json));
        return { products };
    },

    methods: {
        // Sorts products from low to high by key value, optional parameters key2 for products.rating.rate
        sortAsc(products, key, key2) {
            products.sort((a, b) => {
                if (key2 === undefined) {
                    a = a[key];
                    b = b[key];
                } else {
                    a = a[key][key2];
                    b = b[key][key2];
                }
                return a - b;
            });
        },

        // Sorts products from high to low by key value, optional parameters key2 for products.rating.rate
        sortDesc(products, key, key2) {
            products.sort((b, a) => {
                if (key2 === undefined) {
                    a = a[key];
                    b = b[key];
                } else {
                    a = a[key][key2];
                    b = b[key][key2];
                }
                return a - b;
            });
        },

        // Selects which sorting to use
        sortingMode(value) {
            switch (value) {
                case 'priceAsc':
                    this.sortAsc(this.products,'price')
                    break;

                case 'priceDesc':
                    this.sortDesc(this.products,'price')
                    break;
                case 'ratings':
                    this.sortDesc(this.products, 'rating', 'rate')
                    break;
            }
        },
    },
};
</script>

<style scoped>
.product-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
</style>
