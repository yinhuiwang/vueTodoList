<template>
    <li :style="{'background-color': bgColor}" @mousemove="showDelBtn(true)" @mouseout="showDelBtn(false)">
        <input type="checkbox" v-model="todo.flag" />
        <label >{{todo.title}}</label>
        <button type="button" v-show="isShowDelBtn" @click="delteLi">删除</button>
    </li>
</template>

<script>
import PubsubJs from 'pubsub-js';

export default {
    name: 'ItemLi',
    props: {
        todo: Object,
        index: {
            type: Number,
            required: true 
        }
    },
    data(){
        return {
            isShowDelBtn: false,
            bgColor: '#fff'
        }
    },
    methods: {
        showDelBtn(is){
            this.isShowDelBtn = is;
            this.bgColor = is ? 'red' : '#fff';      
        },
        delteLi: function(){
            console.log('触发item删除按钮点击事件！！！');
            PubsubJs.publish('delteLi', this.index);
        }
    }
}
</script>

<style scoped>

</style>