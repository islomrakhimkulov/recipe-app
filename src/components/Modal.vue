<template>
    <div>
        <div>
            <b-modal id="modalPopover" title="Modal with Popover" ok-only>
                <h2> {{ recipeItem.recipe.recipe.label }} </h2>
                <p>CuisineType: {{ recipeItem.recipe.cuisineType}} </p>
                <p>TotalWeight: {{ recipeItem.recipe.totalWeight.toFixed(2)}} </p>
                <p>Source: {{ recipeItem.recipe.source}} </p>
                <p>MealType: {{recipeItem.recipe.mealType}} </p>
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
}
</script>

<style>
    .modal-header {
        display: none !important;
    }
    .modal-footer {
        border-top: 0px !important;
    }
</style>
