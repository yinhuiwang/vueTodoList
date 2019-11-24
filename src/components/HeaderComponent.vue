<template>
    <div>
        <input v-model="item" @keydown.enter="headAddItem" 
            type="text" placeholder="新增内容，回车键确定"/>
    </div>
</template>

<script>
export default {
    name: 'Header',
    data(){
        return {
            item: ''
        }
    },
    methods: {
        headAddItem(){
            // 添加内容
            this.$emit('headAddItem', {'title': this.item, 'flag': false})
            // 清空输入框
            this.item = '';
        }
    }
}
</script>

<style scoped>

</style>