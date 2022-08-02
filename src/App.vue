<template>
  <div id="app">
    <Form @onSubmit="onSubmitForm" />
    <TotalBudget :totalBudget="totalBudget" />
    <SortBudget :list="list" @onFilter="filterBudgetList"/>
    <BudgetList :list="visibleList" :filter="filter" @onDeleteItem="onDeleteItem"/>
    <img class="cat-img" src="./assets/cat.png" alt="cat">
  </div>
</template>

<script>
import BudgetList from './components/BudgetList.vue';
import TotalBudget from './components/TotalBudget.vue';
import Form from './components/Form.vue';
import SortBudget from './components/SortBudget.vue'

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBudget,
    Form,
    SortBudget
  },
  data: ()=>({
    list: {
      1: {
        type: "INCOME",
        value: 100,
        comment: 'Some comment',
        id: 1
      },
      2: {
        type: "OUTCOME",
        value: 50,
        comment: 'Some outcome comment',
        id: 2
      }
    },
    visibleList: {
      1: {
        type: "INCOME",
        value: 100,
        comment: 'Salary',
        id: 1
      },
      2: {
        type: "OUTCOME",
        value: 50,
        comment: 'Shoping',
        id: 2
      }
    },
    filter: {
      value: 'ALL'
    }
  }),
  computed: {
      totalBudget() {
        let totalBudget = 0;
        let color = 'red';
        Object.values(this.list).forEach(item=>{
          if(item.type == 'INCOME') {
            totalBudget += item.value
          } else {
            totalBudget -= item.value
            
          }
        })
        if (totalBudget>0){
          color = 'green';
        } else if (totalBudget === 0) {
          color = 'black'
        } else {
          color = 'red'
        }
        return {totalBudget, color}
      }
    },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
      this.filterBudgetList(this.filter.value)
    },
    onSubmitForm(data){
      const newObj = {
        ...data,
        id: String(Math.random()),
      };

      this.$set(this.list, newObj.id, newObj)
      this.filterBudgetList(this.filter.value)
    },
    filterBudgetList(data){
      console.log(typeof(data));
      if (data === 'ALL') {
        this.visibleList = JSON.parse(JSON.stringify(this.list));
      } else {
        console.log('sdsd222')
        this.visibleList = Object.assign({},Object.values(this.list).filter(item=>item.type==data))
      }
      this.filter.value = data;
    },
  },
  // watch: {

  // }
}
</script>

<style lang="scss">
#app {
  // font-family: Avenir, Helvetica, Arial, sans-serif;
  // -webkit-font-smoothing: antialiased;
  // -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.cat-img {
  position: absolute;
  right: 50px;
  bottom: 50px;
}
</style>
