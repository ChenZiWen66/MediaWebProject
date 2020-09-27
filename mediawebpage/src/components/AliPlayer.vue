<template>
    <div id="aliPlayer">
<!--        <button @click="addPlayer">aaa</button>-->
    </div>
</template>

<script>
    import {globalBus} from "./GlobalBus";

    export default {
        name: "AliPlayer",
        mounted() {
            this.addPlayer();
        },
        data() {
            return {
                player: {}
            }
        },
        methods: {
            addPlayer() {
                //    0.接收来自Browser传递过来的信息[title,url]
                //    1.在template中加上<div class="prism-player" id="J_prismPlayer"/>
                //    2.新建一个Aliplayer
                //    第一步:
                let _this = this;
                globalBus.$on("videoInfo_fromMediaBrowser", function (videoInfo) {
                    let videotitle = videoInfo[0];
                    let videourl = videoInfo[1];
                    let txt3 = document.createElement("div");
                    txt3.setAttribute('class', 'prism-player');
                    txt3.setAttribute('id', videotitle + '-player');
                    $("#aliPlayer").html(txt3);

                    _this.player = new Aliplayer({
                        id: videotitle + '-player',
                        width: '100%',
                        autoplay: false,
                        //支持播放地址播放,此播放优先级最高
                        source: videourl,
                        // cover:_this.coverUrl
                    })
                });

            }
        }
    }
</script>

<style scoped>

</style>