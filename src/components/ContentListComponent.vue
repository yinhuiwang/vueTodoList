<template>
    <div>
        <ul>
            <ItemLi v-for="(value, index) in todos" :key="todosKeys[index]" 
            :todo="value" :index="index" 
            />
        </ul>
    </div>
</template>

<script>
import ItemLi from './ItemLi.vue'
import shortId from 'shortid'

export default {
    name: 'ContentList',
    components: {
        ItemLi
    },
    data(){
        return {
            todosKeys: []
        }
    },
    props: {
        todos: {
            type: Array,
            required: true,
            default: []
        }
    },
    mounted() {
        this.todosKeys = this.todos.map(() => {
            return shortId.generate();
        })
    },
}
</script>

<style scoped>

</style>