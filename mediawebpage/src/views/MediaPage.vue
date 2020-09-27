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
                               video-title="光耀喝酒"
                               describe="光耀喝酒的视频"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E5%85%89%E8%80%80%E5%96%9D%E9%85%92.mp4"/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%B8%B8%E6%88%8F%E7%8E%8B%E5%B0%81%E9%9D%A21.jpg"
                               video-title="游戏王12"
                               describe="游戏王12集的描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%B8%B8%E6%88%8F%E7%8E%8BSEVENS%E7%AC%AC%E5%8D%81%E4%BA%8C%E8%AF%9D.mp4"/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%B8%B8%E6%88%8F%E7%8E%8B%E5%B0%81%E9%9D%A22.jpg"
                               video-title="游戏王14"
                               describe="游戏王14集的描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/SEVENS%20014..mp4"/>
                <media-browser img-src="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%AD%A6%E6%B1%89%E5%B0%81%E9%9D%A2.jpg"
                               video-title="活动视频"
                               describe="这是活动视频描述"
                               video-url="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E6%B4%BB%E5%8A%A8%E8%A7%86%E9%A2%91.mp4"/>
            </div>
            <div class="col-md-1 advertise">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
                <img src="../assets/advertise.png" alt="../../public/xiaolan.jpg">
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
                sheet: 'picture'
            }
        },
        components: {
            Carousel, MediaBrowser,VideoModal
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