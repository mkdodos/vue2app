<template>
  <form @submit.prevent="FormHandler">
    
    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">日期</label>
      <input type="date" class="form-control" v-model="formData.date" />
    </div>

    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">項目</label>
      <input type="text" class="form-control" v-model="formData.note" />
    </div>

    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">金額</label>
      <input
        type="number"
        class="form-control"
        v-model="formData.value"
        id=""
      />
      <div id="emailHelp" class="form-text">
        We'll never share your email with anyone else.
      </div>
    </div>

   


    <div class="d-grid gap-2">
      <input type="submit" class="btn btn-primary" value="add" />
    </div>
  </form>
</template>

<script>
import { reactive } from "vue";
// import bootstrap from 'bootstrap'
export default {
  props: {},
  setup(props, { emit }) {
    const formData = reactive({
      value: null,
      note: null,
      date: null
    });
    function FormHandler() {
      emit("add-income", {
        value: formData.value,
        note: formData.note,
        date: formData.date
      });

      formData.value = null;
      formData.note = null;
      // formData.date = null;
    }
    return {
      FormHandler,
      formData,
    };
  },
};
</script>

<style>
</style>