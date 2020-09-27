<template>
    <div id="videomodal" class="modal fade" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                    <h4 class="modal-title">Modal title</h4>
                </div>
                <div class="modal-body">
                    <p>One fine body&hellip;</p>
<!--                    <AliPlayer videoUrl="https://czwhub.oss-cn-shanghai.aliyuncs.com/%E5%85%89%E8%80%80%E5%96%9D%E9%85%92.mp4"/>-->
                    <AliPlayer/>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary">Save changes</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import AliPlayer from "./AliPlayer";

    export default {
        name: "videoModal",
        components:{
            AliPlayer
        }
    }
</script>