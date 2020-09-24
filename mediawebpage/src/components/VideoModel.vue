<template>
    <!-- Modal -->
    <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                    <h4 class="modal-title" id="myModalLabel">这是一个视频</h4>
                </div>
                <div class="modal-body">
                    <video  id="modelVideo" controls>
                        <source src="../../public/drink.mp4">
                        您的浏览器不支持，请升级您的浏览器
                    </video>
                    <p>
                        光耀喝酒
                    </p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary" data-dismiss="modal">嗯，好</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "VideoModel"
    }
</script>

<style scoped>
    #modelVideo{
        height: 300px;
        width: 400px;
        background-color: gray;
    }
</style>