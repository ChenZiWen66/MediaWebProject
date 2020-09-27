<template>
    <div class="media col-md-12 fff">
        <div class="media-left media-middle">
            <img id="mediaBrowserImg" class="media-object img-circle" :src="imgSrc" :alt="videoTitle"
                 data-toggle="modal" data-target="#videomodal" @click="touchImg">
        </div>
        <div class="media-body">
            <h4 class="media-heading">{{videoTitle}}</h4>
            <p>{{describe}}</p>
        </div>
    </div>
</template>

<script>
    import {globalBus} from "./GlobalBus";

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
            videoUrl: ''
        },
        methods: {
            touchImg() {
                /**
                 * 点击图片事件：
                 * 1.向阿里播放器组件发送信息：[视频标题、视频播放地址]，接收到信息后阿里播放器调用修改方法
                 * 2.弹出模态框
                 */
                let _this = this;
                console.log("点击了图片" + _this.videoTitle);
                globalBus.$emit("videoInfo_fromMediaBrowser",[_this.videoTitle,_this.videoUrl]);
                console.log("修改播放内容为",_this.videoUrl);
                $("#videomodal").find(".modal-title").text(_this.videoTitle).on("shown.bs.modal");;
                console.log("修改模态框标题为",_this.videoTitle);
                // $("#videomodal").on("shown.bs.modal");
                console.log("弹出模态框");
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