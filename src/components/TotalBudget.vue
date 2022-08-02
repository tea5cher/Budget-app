<template>

<div class="total-budget" :class="totalBudget.color">Total balance: {{totalBudget.totalBudget}}</div>

</template>



<script>
// console.log(totalBudget)
export default {
    name: 'TotalBudget',
    props: {
        totalBudget: {
            type: Object,
            default: ()=>({})
        }
    },
    // computed: {
    //     totalBudgetColor(){
    //         console.log(this.totalBudget);
    //     }
    // },
    methods:{
        changeBg(){
            console.log(this.totalBudget);
        }
    }
}
</script>



<style lang="scss" scoped>
    .total-budget {
        font-style: 26px;
        text-transform: uppercase;
        padding: 20px;
        text-align: center;
        width: 500px;
        margin: auto;
        color: white;
        margin-top: 20px;
        font-weight: 600;
    }
    .red {
        background-color: #ee5c5c;
        // color: white;
    }
    .green {
        background-color: rgb(58, 211, 58);
        // color: white;
    }
    .black {
        background-color: black;
        // color: white
    }
</style>