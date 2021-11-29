<template>
    <div class="container py-5">
        <b-input-group class="mt-3" @click="recipeButton()">
            <b-form-input placeholder="Search"></b-form-input>
            <b-button class="danger">Search</b-button>
        </b-input-group>
        <h2 class="p-4 text-white text-center">Recipe App with Edamam API</h2>
        <div class="row gy-3">
           <div class="col-md-6 m-auto">
                <div class="card mb-4" v-for="(info,index) in this.test_data" :key="index">
                    <img :src="info.recipe.image" class="card-img-top " alt="card-image">
                    <div class="card-body">
                        <div class="card-title h2 fw-bolder">{{ info.recipe.label }}</div>
                        <span class="fw-bold h4">Ingredients:</span><br>
                        <ul>
                            <li v-for="(ingredient, index) in info.recipe.ingredientLines" :key="index">
                                {{ ingredient }}
                            </li>
                        </ul>
                        <p class="ps-1 h6">Calories: {{ info.recipe.calories.toFixed(2) }}</p>
                    </div>
                </div>
            </div>
            <!-- <div class="col-md-6">
                <div class="card">
                    <img :src="this.test_data[1].recipe.image" class="card-img-top " alt="card-image">
                    <div class="card-body">
                        <div class="card-title h4 fw-bolder">{{ this.test_data[1].recipe.label }}</div>
                        <span class="fw-bold">Ingredients:</span><br>
                            <ul>
                                <li v-for="(ingredient, index) in this.test_data[1].recipe.ingredientLines" :key="index">
                                    {{ ingredient }}
                                </li>
                            </ul>
                        <p class="ps-1 h6">Calories: {{ this.test_data[1].recipe.calories.toFixed(2) }}</p>
                    </div>
                </div>
            </div> -->
        </div>
    </div>
</template>

<script>
export default {
    name: 'RecipeApp',
    data: () => ({
        test_data: [],
    }),
    methods: {
        recipeButton(){
            this.sendApiRequest();
            console.log(this.test_data[0].recipe.label);
        },
        async sendApiRequest() {
           const API_ID = "811fd5df"
           const API_KEY = "53a0c98c7c38b1776435f72a5e256d02"
           const response = await fetch(`https://api.edamam.com/search?app_id=${ API_ID }&app_key=${ API_KEY }&q=chicken`)
           const data = await response.json();
           this.test_data = data.hits;
            console.log(this.test_data);

            console.log(this.test_data[0]);

            // console.log(this.test_data[0].recipe.label);
            console.log(this.test_data[0].recipe);

            
            // this.test_data.forEach((item,index) => {
            //     console.log(item,index);
            // });


            // .then(response => response.json())
            // .then(json_data => this.test_data = json_data.test_data);
            // console.log(response);
        },
    },
    mounted(){
        this.sendApiRequest();
    }
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
