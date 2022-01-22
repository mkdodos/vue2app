<template>
  <Header :totalIncome="state.totalIncome" />  
  <Form @add-income="AddIncome" />
  <IncomeList :state="state" />
</template>

<script>
import { reactive, computed } from 'vue';
import Header from "./components/Header";
import Form from "./components/Form";
import IncomeList from "./components/IncomeList";

export default {
  
  components:{
    Header,
    Form,
    IncomeList,
    
  },
  setup() {
    const state = reactive({
      income: [
        // {
        //   value: 400
        // },
        // {
        //   value: 500
        // },
      ],
      totalIncome: computed(() => {
          let temp = 0;
          if (state.income.length > 0) {
            for (let i = 0; i < state.income.length; i++) {
              temp += state.income[i].value;
            }
            return temp;
          } else {
            return 0;
          }
        })        
    });

    function AddIncome(data) {
      state.income = [...state.income,{
        id: Date.now(),
        desc: data.desc,
        value: data.value,
        date: data.date
      }]
      console.log(state.income);
    }

    function removeItem(id) {
       console.log(id)
      state.income = state.income.filter(v => v.id != id);
    }
    
    
    return {
      // Header,
      // Form,
      removeItem,
      AddIncome,
      IncomeList,
      state
    }
  }
}
</script>

<style>
  * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
  }
  body {
    background: #EEE;
  }
</style>
