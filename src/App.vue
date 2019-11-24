<template>
    <div id="app">
        <HeaderComponent ref="headerComponentRef" />
        <ContentListComponent :todos="todos" />
        <FootedComponent :todos="todos" :isCheckedAllTodoFun="isCheckedAllTodo" :clearCheckedTodoFun="clearCheckedTodo"/>
    </div>
</template>

<script>
// 引入插件
import PubsubJs from 'pubsub-js'

// 引入vue组件
import HeaderComponent from './components/HeaderComponent';
import FootedComponent from './components/FootedComponent';
import ContentListComponent from './components/ContentListComponent';

export default {
    name: 'app',
    components: {
        HeaderComponent,
        FootedComponent,
        ContentListComponent
    },
    data(){
        return {
            todos: [
                {title: '学习vue', flag: false},
                {title: '写案例', flag: false},
                {title: '综合复习', flag: false}
            ]
        }
    },
    mounted() {
        // 实例属性的调用
        this.$refs.headerComponentRef.$on('headAddItem', this.addTodo);
        // 订阅消息
        PubsubJs.subscribe('delteLi', (msg, data) => {
            this.appLiDel(data);
        });
    },
    methods: {
        appLiDel(index){
            this.todos = this.todos.filter((value, i) => {
                return index !== i;
            })
        },
        addTodo(todo){
            this.todos.unshift(todo);
        },
        isCheckedAllTodo(is){
            this.todos.forEach((todo) => { todo.flag = is });
        },
        clearCheckedTodo(){
            this.todos = this.todos.filter((value) => {
                return !value.flag;
            }) 

        }
    }
}
</script>

<style>
</style>
