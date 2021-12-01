<template>
    <div>
        <div>
            <b-modal id="modalPopover" title="Modal with Popover" ok-only>
                <h2> {{ recipeItem[0].recipe.label }} </h2>
                <p>CuisineType: {{ recipeItem[0].recipe.cuisineType[0]}} </p>
                <p>TotalWeight: {{ recipeItem[0].recipe.totalWeight.toFixed(2)}} </p>
                <p>Source: {{ recipeItem[0].recipe.source}} </p>
                <p>MealType: {{recipeItem[0].recipe.mealType[0]}} </p>
            </b-modal>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    props: {
        recipeItem: {
            type: Array,
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
