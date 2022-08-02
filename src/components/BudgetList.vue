<template>
    <div class="budget-list-wrap">
        <el-card>
            <div class="bold">{{header+ ":" + " " + filter.value}}</div>
            <hr>
            <template v-if="!isEmpty">
                <!-- <div class="list-item" v-for="(item, prop) in list" :key="prop">
                    <span class="budget-comment">{{item.comment}}</span>
                    <span class="budget-value">{{item.value}}</span>
                    <ElButton type="danger" size="mini" @click="deleteItem(item.id)">Delete</ElButton>
                </div> -->
                <BudgetListItem @deleteItem="onDelete" :list='list' />
            </template>
            <el-alert v-else type='info' :title="emptyTitle" :closable="false"/>
        </el-card>
    </div>
</template>

<script>

import BudgetListItem from './BudgetListItem.vue'

export default {
    name: 'BudgetList',
    components: {
        BudgetListItem,
    },
    props: {
        list: {
            type: Object,
            default: ()=> ({}),
        },
        filter: {
            type: String,
            default: 'ALL'
        }
    },
    data: ()=> ({
        header: 'Budget list',
        emptyTitle: "Budget list is empty"
    }),
    computed: {
        isEmpty() {
            return !Object.keys(this.list).length;
        }
    },
    methods: {
        onDelete(id){
            this.$emit("onDeleteItem", id)
        }
    }
}

</script>

<style lang="scss" scoped>
.budget-list-wrap {
    max-width: 500px;
    margin: 20px auto;
    transition: all 0.6s;
}
.bold {
    font-weight: 700 !important;
}

</style>