<template>
    <div class="container-fluid">
        <div class="row">
            <ul class="nav nav-tabs col-md-12">
                <li role="presentation" :class="{'active':sheet==='home'}" @click="setSheet('home')"><a href="#">首页</a>
                </li>
                <li role="presentation" :class="{'active':sheet==='picture'}" @click="setSheet('picture')"><a href="#">图片</a>
                </li>
                <li role="presentation" :class="{'active':sheet==='video'}" @click="setSheet('video')"><a
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
                <button type="button" class="btn btn-primary col-md-2 col-md-offset-10" data-toggle="modal"
                        data-target="#uploadFileModal" @click="clickUploadButton">上传视频
                </button>
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
    import {globalBus} from "../components/GlobalBus";

    export default {
        name: "MediaPage",
        data() {
            return {
                // 导航栏标签
                sheet: 'picture',
                //视频数量
                videoInfoCount: 0,
                //当前页面数
                currentPage: 1,
                //页面大小
                pageSize: 5,
                //最大页面数
                maxPage: 1,
                // 视频信息列表
                videoInfoList: []
            }
        },
        components: {
            Pagination, Carousel, MediaBrowser, VideoModal, UploadFileModal
        },
        async mounted() {
            let _this = this;
            //获取信息数目
            await _this.$http.get("http://localhost:9001/getCount").then(function (response) {
                _this.videoInfoCount = response.data.count;
            });
            //初始化第一面内容
            this.getVideoInfoList(_this.currentPage, _this.pageSize);
            if (_this.videoInfoCount !== 0) {
                _this.maxPage = Math.ceil(_this.videoInfoCount / _this.pageSize);
                globalBus.$emit("PaginationMaxPage",_this.maxPage);
            }
            //接收并更新当前页面
            globalBus.$on('videoInfoCurrentPage', function (currentPage) {
                _this.currentPage = currentPage;
            })
        },
        watch: {
            /**
             * 监听当前页面,每次当前页面数发生改变时，更新视频列表
             */
            currentPage() {
                let _this = this;
                _this.getVideoInfoList(_this.currentPage, _this.pageSize);
            }
        },
        methods: {
            setSheet(sheet) {
                // 设置导航栏标签
                this.sheet = sheet;
            },
            clickUploadButton() {
                console.log("点击了上传文件");
                $("#uploadFileModal").on("shown.bs.modal");
            },
            getVideoInfoList(currentPage, pageSize) {
                //获取视频列表
                let _this = this;
                let formData = new window.FormData();
                formData.append("currentPage", currentPage);
                formData.append("pageSize", pageSize);
                this.$http.post("http://localhost:9001/getInfo", formData).then(function (response) {
                    _this.videoInfoList = response.data;
                })
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

    .videoContent {
        padding: 0;
        margin-bottom: 2px;
    }
</style>