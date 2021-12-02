<template>
    <div>
        <div>
            <b-modal id="modalPopover" title="Modal with Popover" ok-only>
                <h2> {{ recipeItem.recipe.label }} </h2>
                <div class="recipe-info">
                    <p>Calories: {{ recipeItem.recipe.calories.toFixed(2) }}</p>
                    <p> Cautions: {{ recipeItem.recipe.cautions[0] }} </p>
                    <p>CuisineType: {{ recipeItem.recipe.cuisineType[0] }} </p>
                    <p>DietLabels: {{ recipeItem.recipe.dietLabels[0] }} </p>
                    <p>TotalWeight: {{ recipeItem.recipe.totalWeight.toFixed(2) }} </p>
                    <p>Source: {{ recipeItem.recipe.source}} </p>
                    <p>MealType: {{ recipeItem.recipe.mealType[0] }} </p>
                </div>
            </b-modal>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    props: {
        recipeItem: {
            type: Object,
            default: () => ({
                recipe: Object,
            }),
        },
    },
    data: () => ({
        recipe: Object,
    }),
    
}
</script>

<style>
    .modal-header {
        display: none !important;
    }
    .modal-footer {
        border-top: 0px !important;
    }
    .recipe-info {
        padding-left: 0.25rem !important;
        font-size: 1.1rem;
        font-weight: 700;
    }
</style>

// v-b-modal.modalPopover for opening Modal 
