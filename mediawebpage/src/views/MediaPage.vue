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
                <carousel/>
                <div v-for="videoInfo in videoInfoList">
                    <media-browser :img-src=videoInfo.imgSrc
                                   :video-title=videoInfo.videoTitle
                                   :describe=videoInfo.describe
                                   :video-url=videoInfo.videoUrl />
                </div>
            </div>
            <div class="col-md-1 advertise">
                <img src="../assets/advertise.png" alt="广告">
                <img src="../assets/advertise.png" alt="广告">
                <img src="../assets/advertise.png" alt="广告">
            </div>
        </div>
        <video-modal/>
    </div>
</template>

<script>
    import Carousel from "../components/Carousel";
    import MediaBrowser from "../components/MediaBrowser";
    import VideoModal from "../components/VideoModal";

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
            Carousel, MediaBrowser, VideoModal
        },
        mounted() {
            let _this = this;
            this.$http.get("videoInfo.json").then(function (response) {
                console.log(response.data);
                _this.videoInfoList = response.data;
            })
        },
        methods: {
            setsheet(sheet) {
                // 设置导航栏标签
                this.sheet = sheet;
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
</style>