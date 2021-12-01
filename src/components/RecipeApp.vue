<template>
    <div class="container py-5">
        <Modal :recipe-item="test_data"/>
        <b-input-group class="mt-3">
            <b-form-input v-model="search" placeholder="Search"></b-form-input>
            <b-button @keyup="onSearch()">Search</b-button>
        </b-input-group>
        <h2 class="p-4 text-white text-center">Recipe App with Edamam API</h2>
        <div class="row gy-3">
           <div class="col-md-6 m-auto">
                <div class="card mb-4 shadow" v-for="(info,index) in filteredList" :key="index" v-b-modal.modalPopover>
                    <img :src="info.recipe.image" class="card-img-top" alt="card-image">
                    <div class="card-body">
                        <div class="h2 fw-bolder">{{ info.recipe.label }}</div>
                        <span class="fw-bold h4">Ingredients:</span><br>
                        <ul>
                            <li v-for="(ingredient, index) in info.recipe.ingredientLines" :key="index">
                                {{ ingredient }}
                            </li>
                        </ul>
                        <div class="d-flex justify-content-between align-items-center">
                            <p class="ps-1 h6">Calories: {{ info.recipe.calories.toFixed(2) }}</p>
                            <b-button v-b-modal.modalPopover variant="outline-info" size="sm" @click="showModal()">Ba'tafsil</b-button>
                        </div>
                    </div> 
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import debounce from "debounce";
import Modal from './Modal.vue';
export default {
    name: 'RecipeApp',
    components: {
        Modal
    },
    data: () => ({
        test_data: [],
        searchValue: "chicken",
        debouncedSearch: null,
    }),
    computed: {
        filteredList() {
            return this.test_data.filter((item) => {
                const recipe = item.recipe;
                return recipe.label.toLowerCase().includes(this.search.toLowerCase())
            });
        },
        search: {
            get() {
                return this.searchValue;
            },
            set(value) {
                this.searchValue = value;
                this.onSearch();
            }
        },
        requestUrl() {
            const API_ID = "811fd5df";
            const API_KEY = "53a0c98c7c38b1776435f72a5e256d02";
            const url = new URL("https://api.edamam.com/search");
            let params = {
                app_id: API_ID,
                app_key: API_KEY
            };

            if (this.search && this.search.trim()) {
                params.q = this.search;
            }

            url.search = new URLSearchParams(params).toString();
            return url;
        }
    },
    methods: {
        async sendApiRequest() {
           const response = await fetch(this.requestUrl);
           const data = await response.json();
           this.test_data = data.hits;
        },
        recipeButton(){
            this.sendApiRequest();
        },
        onSearch() {
            if (!this.debouncedSearch) {
                this.debouncedSearch = debounce(this.sendApiRequest, 300);
            }

            this.debouncedSearch();
        },
        showModal() {
            console.log(this.test_data);
        },
    },
    mounted(){
        this.sendApiRequest();
    },
}
</script>

<style>
.container{
  max-width: 700px !important;
  width: 100%;
  margin: auto;
}
ul li {
    list-style: none;
}
</style>
