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
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
            </div>
            <div class="col-md-10 innerContent">
                <carousel/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/xiaolan.jpg"
                               video-title="视频1"
                               describe="这是视频1的描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E5%85%89%E8%80%80%E5%96%9D%E9%85%92.mp4"/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/xiaolan.jpg"
                               video-title="视频2"
                               describe="这是视频2的描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E5%85%89%E8%80%80%E5%96%9D%E9%85%92.mp4"/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/xiaolan.jpg"
                               video-title="视频3"
                               describe="这是视频3的描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%B4%BB%E5%8A%A8%E8%A7%86%E9%A2%91.mp4"/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/xiaolan.jpg"
                               video-title="视频4"
                               describe="这是视频4的描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%B4%BB%E5%8A%A8%E8%A7%86%E9%A2%91.mp4"/>
            </div>
            <div class="col-md-1 advertise">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
            </div>
        </div>
    </div>
</template>

<script>
    import Carousel from "../components/Carousel";
    import MediaBrowser from "../components/MediaBrowser";

    export default {
        name: "MediaPage",
        data() {
            return {
                sheet: 'picture'
            }
        },
        components: {
            Carousel, MediaBrowser
        },
        methods: {
            setsheet(sheet) {
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