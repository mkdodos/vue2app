<template>
  <div class="container">
    <h1>
      <span class="badge bg-secondary">{{ state.total }}</span>
    </h1>

    <Form2 @add-income="AddIncome" />
    <hr />

    <!-- 
      remove-income 子元件定義事件
      :income="obj" 綁定資料,子元件可透過 props 接收
    -->
    <ul class="list-group list-group-flush">
      <income-list-2
        v-for="obj in state.income"
        :key="obj.value"
        :income="obj"        
        @remove-income="removeItem"
      />
    </ul>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import Form2 from "./components/Form2";
import IncomeList2 from "./components/IncomeList2";
export default {
  setup() {
    const state = reactive({
      income: [],
      total: computed(() => {
        let temp = 0;
        for (let i = 0; i < state.income.length; i++) {
          temp += state.income[i].value;
        }
        return temp;
      }),
    });  

    function removeItem(id) {      
      // 使用陣列的 filter 傳回符合條件的新陣列 
      state.income = state.income.filter(v => v.id != id)
    }
    function AddIncome(obj) {      
      state.income = [
        ...state.income,
        {
          id: Date.now(),
          note: obj.note,
          value: obj.value,
          date: obj.date,
        },
      ];
    }

    return {
      state,
      Form2,
      AddIncome,
      removeItem,
    };
  },
  components: {
    Form2,
    IncomeList2,
  },
};
</script>

<style>
.container {
  margin-top: 20px;
}
</style>