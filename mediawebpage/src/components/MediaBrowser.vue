<template>
    <div class="media col-md-12 fff">
        <div class="media-left media-middle">
            <img id="mediaBrowserImg" class="media-object img-circle" :src="imgSrc" :alt="videoTitle" @click="touchImg">
        </div>
        <div class="media-body">
            <h4 class="media-heading">{{videoTitle}}</h4>
            <p>{{describe}}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "MediaBrowser",
        props: {
            //图片路径
            imgSrc: '',
            //视频标题
            videoTitle: '',
            //视频描述
            describe: '',
            // 视频路径
            videoUrl:''
        },
        methods:{
            touchImg(){
                let _this=this;
                console.log("点击了图片"+_this.videoTitle)
            }
        }
    }
</script>

<style scoped>
    .media img {
        width: 100px;
        height: 100px;
        margin: 5px;
    }

    .fff {
        background-color: beige;
    }
</style>