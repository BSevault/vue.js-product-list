<template>
    <h1>Our products</h1>
    <button @click="displayCategory('men')" >Category</button>

    <div class="sorting-wrapper">

        <div class="check-box">
            <check-box 
            v-for="(cat, index) of categories"
            :key="index"
            :cat="cat"
            @change="test($event.target.value)" 
            ></check-box>
        </div>

        <div class="sorting-select">
            <sorting-select 
                @sortingOption="sortingMode($event)"
            ></sorting-select>
        </div>
    </div>


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
import CheckBox from "./components/CheckBox.vue";

export default {
    name: "ProductList",
    components: {
        ProductCard,
        SortingSelect,
        CheckBox
        
    },

    data() {
        const categories = ['men', 'women', 'jewelery', 'electronics'];
        return {categories};
    },

    setup() {
        // Getting the product list as a json with fetch(), and pass it to ProductCard component as props
        const products = ref(null);

        fetch("https://fakestoreapi.com/products")
            .then((res) => res.json())
            .then((json) => (products.value = json));
        return { products };
    },

    methods: {

        test(texte) {
            console.log(texte);
        },

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

        // Selects category to display
        displayCategory(categories) {
            const products = document.getElementsByClassName('product-card');
            for (let i = 0 ; i<products.length ; i++) {
                const search = products[i].classList.value.substring(0,4)
               if (search.includes(categories, 0)) {
                   products[i].style.display = "flex"
                } else {
                    products[i].style.display = "none"
               }
            }
        }
    },
};
</script>

<style scoped>
.product-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.sorting-wrapper{
    display: flex;
    justify-content: center;
    align-items: center;
}

.check-box {
    display: flex;
    margin: 0 10px;
}

.sorting-select {
    margin: 0 10px;
}
</style>
