<template>
    <div id="app">
        <HeaderComponent ref="headerComponentRef" />
        <ContentListComponent :todos="todos" />
        <!-- <FootedComponent :todos="todos" :isCheckedAllTodoFun="isCheckedAllTodo" :clearCheckedTodoFun="clearCheckedTodo"/> -->
        <FootedComponent>
             <span slot="footedIsCheckedAll">全选<input type="checkbox" v-model="isCheckedAll"/></span>
             <span slot="footedContent">说明信息：{{successful}}/ {{allTodosCount}}</span>
             <slot slot="footedButton" name="footedButton">
                 <button type="button" @click="clearCheckedTodo">清除已完成的任务</button>
             </slot>
        </FootedComponent>
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
                this.isCheckedAllTodo(value);
            }
        }
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
