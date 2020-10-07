<template>
    <div class="container-fluid">
        <div class="row">
            <ul class="nav nav-tabs col-md-12">
                <li role="presentation" :class="{'active':sheet==='home'}" @click="setsheet('home')"><a href="#">首页</a>
                </li>
                <li role="presentation" :class="{'active':sheet==='picture'}" @click="setsheet('picture')"><a href="#">图片</a>
                </li>
                <li role="presentation" :class="{'active':sheet==='video'}" @click="setsheet('video')"><a
                        href="#">视频</a></li>
            </ul>
        </div>
        <div class="row">
            <div class="col-md-1 advertise">
                <img src="../assets/advertise.png" alt="广告">
                <img src="../assets/advertise.png" alt="广告">
                <img src="../assets/advertise.png" alt="广告">
            </div>
            <div class="col-md-10 innerContent">
                <!--轮播框-->
                <carousel/>
                <!--上传按钮-->
                <button type="button" class="btn btn-primary col-md-2 col-md-offset-10" data-toggle="modal" data-target="#uploadFileModal" @click="clickUploadButton">上传视频</button>
                <!--视频内容-->
                <div v-for="videoInfo in videoInfoList" class="col-md-12 videoContent">
                    <media-browser :img-src=videoInfo.imgSrc
                                   :video-title=videoInfo.videoTitle
                                   :describe=videoInfo.describe
                                   :video-url=videoInfo.videoUrl />
                </div>
                <!--分页栏-->
                <div class="col-md-12">
                    <Pagination/>
                </div>
            </div>
            <div class="col-md-1 advertise">
                <img src="../assets/advertise.png" alt="广告">
                <img src="../assets/advertise.png" alt="广告">
                <img src="../assets/advertise.png" alt="广告">
            </div>
        </div>
        <video-modal/>
        <upload-file-modal/>
    </div>
</template>

<script>
    import Carousel from "../components/Carousel";
    import MediaBrowser from "../components/MediaBrowser";
    import VideoModal from "../components/VideoModal";
    import UploadFileModal from "../components/UploadFileModal";
    import Pagination from "../components/Pagination";

    export default {
        name: "MediaPage",
        data() {
            return {
                // 导航栏标签
                sheet: 'picture',
                // 视频信息列表
                videoInfoList: []
            }
        },
        components: {
            Pagination,
            Carousel, MediaBrowser, VideoModal,UploadFileModal
        },
        mounted() {
            let _this = this;
            this.$http.get("http://localhost:9001/showInfo").then(function (response) {
                console.log(response.data);
                _this.videoInfoList = response.data;
            })
        },
        methods: {
            setsheet(sheet) {
                // 设置导航栏标签
                this.sheet = sheet;
            },
            clickUploadButton(){
                console.log("点击了上传文件");
                $("#uploadFileModal").on("shown.bs.modal");
            }
        }
    }
</script>

<style scoped>
    .row .advertise img {
        width: 100%;
    }

    .innerContent {
        background-color: wheat;
    }
    .videoContent{
        padding: 0;
        margin-bottom: 2px;
    }
</style>