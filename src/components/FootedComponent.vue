<template>
    <div>
        全选<input type="checkbox" v-model="isCheckedAll"/> 说明信息：{{successful}}/ {{allTodosCount}}
        <button type="button" @click="clearCheckedTodoFun">清除已完成的任务</button>
    </div>
</template>

<script>
export default {
    name: 'Footed',
    props: {
        todos: {
            type: Array,
            required: false
        },
        isCheckedAllTodoFun: Function,
        clearCheckedTodoFun: Function
    },
    computed: {
        successful(){
            return this.todos.filter(function (value) {
                return value.flag
            }).length;
        },
        allTodosCount(){
            return this.todos.length;
        },
        isCheckedAll: {
            get(){
                return this.successful === this.todos.length && this.todos.length > 0;
            },
            set(value){
                this.isCheckedAllTodoFun(value);
            }
        }
    }
}
</script>

<style scoped>

</style>