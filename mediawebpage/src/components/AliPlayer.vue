<template>
    <div  class="prism-player" id="J_prismPlayer"></div>
</template>

<script>
    export default {
        name: "AliPlayer",
        props:{
            videoUrl:'',
            coverUrl:''
        },
        mounted() {
            let _this=this;
            let player = new Aliplayer({
                id: 'J_prismPlayer',
                width: '100%',
                autoplay: false,
                //支持播放地址播放,此播放优先级最高
                source: _this.videoUrl,
                cover:_this.coverUrl
            })
        }
    }
</script>

<style scoped>

</style>