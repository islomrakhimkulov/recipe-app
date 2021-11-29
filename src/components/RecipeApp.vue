<template>
    <div class="container">
        <b-input-group class="mt-3" @click="recipeButton()">
            <b-form-input placeholder="Search"></b-form-input>
            <b-button class="danger">Search</b-button>
        </b-input-group>
        <h2 class="p-4 text-white text-center">Recipe App with Edamam API</h2>
        <div class="row g-3">
           <div class="col-6">
                <div class="card">
                    <img :src="this.test_data[2].recipe.image" class="card-img-top " alt="card-image">
                    <div class="card-body">
                        <h5 class="card-title">{{ this.test_data[2].recipe.label }}</h5>
                        <ul>
                            <li v-for="item in this.test_data[2].recipe.ingredientLines" :key="item">
                                {{ item }}
                            </li>
                        </ul>
                        <p class="ps-1">Calories: {{ this.test_data[2].recipe.calories.toFixed(2) }}</p>
                    </div>
                </div>
            </div>
            <div class="col-6">
                <div class="card">
                    <img :src="this.test_data[0].recipe.image" class="card-img-top " alt="card-image">
                    <div class="card-body">
                        <h5 class="card-title">{{ this.test_data[0].recipe.label }}</h5>
                        <ul>
                            <li v-for="item in this.test_data[0].recipe.ingredientLines" :key="item">
                                {{ item }}
                            </li>
                        </ul>
                        <p class="ps-1">Calories: {{ this.test_data[0].recipe.calories.toFixed(2) }}</p>
                    </div>
                </div>
            </div>
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
        //    console.dir(data);
              console.log(this.test_data);
        //    this.test_data.forEach((value,index)=>{
        //        console.log(value,index);
        //    });

        console.log(this.test_data[0].recipe);

        // console.log(this.test_data[0].recipe.label);
        
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
  max-width: 600px !important;
  width: 100%;
  margin: auto;
}
</style>
