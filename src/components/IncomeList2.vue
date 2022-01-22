<template>   

    <li class="list-group-item">
        <span class="remove-item" @click="removeItem">x</span>
        {{ income.date }}
        [ {{ income.note }} ]
        $ {{ income.value }}
        
    </li>   
 
</template>

<script>
export default {

    // props 接收父層傳來資料
    props: {
        income: Object,
    },
    setup(props, { emit }) {
        function removeItem() {
            // emit 自訂事件傳給父層 (事件名稱, 參數)
            emit("remove-income", props.income.id);     
        }
        return {
            removeItem
        };
    }
};
</script>

<style>
    .remove-item {
        color: #EF2D2D;
        font-weight: 600;
        font-size: 20px;
        line-height: 1;
        text-align: center;
        margin: 0 15px;
    }
</style>