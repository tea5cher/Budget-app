<template>
    <div>
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
            <span class="budget-comment">{{item.comment}}</span>
            <span class="budget-value" 
            :class="
                item.type === 'INCOME'
                    ? 'el-icon-top color-income'
                    : 'el-icon-bottom color-outcome'
            ">
            {{item.value}}
            </span>
            <ElButton type="danger" size="mini" @click="deleteItem(item.id)">Delete</ElButton>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BudgetListItem',
    data(){
        return{

        }
    },
    props: {
        list: {
            type: Object,
            default: ()=> ({}),
        }
    },
    methods: {
        deleteItem(id){
            
            if (confirm('Are you sure?')) {
                 this.$emit("deleteItem", id)
            }
         
        }
    },
     computed: {
        isEmpty() {
            return !Object.keys(this.list).length;
        }
    },
}
</script>

<style lang="scss">
    .list-item {
        display: flex;
        align-items: center;
        padding: 10px 15px;
        transition: all 0.6s;
    }
    .budget-value {
        font-weight: bold;
        margin-left: auto;
        margin-right: 20px;
    }
    .color-income{
        color: #3ad33a;
    }
    .color-outcome{
        color: #F56C6C;
    }
    
</style>