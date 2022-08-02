<template>
    <div class="budget-sort">
        <h3>Sort budget</h3>
        <ElButton @click='budgetFilter' type="primary" size="default">INCOME</ElButton>
        <ElButton @click='budgetFilter' type="primary" size="default">OUTCOME</ElButton>
        <ElButton @click='budgetFilter' type="primary" size="default">ALL</ElButton>
    </div>
</template>

<script>
export default {
    name: 'SortBudget',
    props: {
        list : {
            type: Object,
            default: ()=>({}),
        }
    },
    methods: {
        budgetFilter(e){
            const filter = e.target.textContent; 
            this.$emit('onFilter', filter)
        }
    }
}
</script>


<style lang="scss" scoped>
    .budget-sort{
        margin: 0 auto;
    }
</style>