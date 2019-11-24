<template>
    <div>
        图片1：<img :src="vueLogoImg" alt="我是一张图片"/>
        图片2：<img alt="我是一张图片" src="../assets/logo.png">
        <button type="button" @click="btnClick">删除P标签</button>
    </div>
</template>

<script>
    import vueLogoImg from '../assets/logo.png'
    export default {
        name: "vueImgComponent",
        data(){
            return {
                vueLogoImg: vueLogoImg
            }
        },
        methods: {
            btnClick(){
                this.$emit('btnClick');
                console.log('button被点击了。。。。')
            }
        }
    }
</script>

<style scoped>

</style>