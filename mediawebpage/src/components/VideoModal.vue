<template>
    <div id="videomodal" class="modal fade" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                    <h4 class="modal-title">Modal title</h4>
                </div>
                <div class="modal-body">
                    <AliPlayer ref='player'/>
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
        },
        mounted() {
            let _this=this;
            $('#videomodal').on('hidden.bs.modal', function (e) {
                console.log("模态框关闭了");
                _this.$refs.player.deletePlayer();
            })
        }
    }
</script>