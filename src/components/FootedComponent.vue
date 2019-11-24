<template>
    <div>
        <!-- 全选<input type="checkbox" v-model="isCheckedAll"/> -->
        <slot name="footedIsCheckedAll"></slot>
        <slot name="footedContent"></slot>
        <slot name="footedButton"></slot>
        <!-- 说明信息：{{successful}}/ {{allTodosCount}} -->
        <!-- <button type="button" @click="clearCheckedTodoFun">清除已完成的任务</button> -->
    </div>
</template>

<script>
export default {
    name: 'Footed'
}
</script>

<style scoped>

</style>