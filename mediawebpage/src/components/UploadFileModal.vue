<!--上传文件的模态框-->
<template>
    <div id="uploadFileModal" class="modal fade" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span
                            aria-hidden="true">&times;</span></button>
                    <h4 class="modal-title">上传文件</h4>
                </div>
                <form>
                    <div class="modal-body">
                        <div class="form-group">
                            <div>
                                <label for="fileTitle">文章标题</label>
                                <input type="text" id="fileTitle">
                            </div>
                            <div>
                                <label for="fileDescribe">文章描述</label>
                                <input type="text" id="fileDescribe">
                            </div>
                            <div>
                                <label for="InputFile">选择上传文件</label>
                                <input type="file" id="InputFile">
                            </div>
                            <div>
                                <p class="help-block">填写上方信息来上传文件</p>
                            </div>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="submit" class="btn btn-primary" data-dismiss="modal" @click="uploadFileInfo">
                            上传视频
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "UploadFileModal",
        methods: {
            async uploadFileInfo() {
                /**
                 * 1.上传文件
                 * 2.在表单中添加信息
                 * 3.访问接口http://localhost:9001/uploadfile
                 */
                console.log("开始上传文件");
                let _this = this;
                let file = document.querySelector('#InputFile').files[0];
                console.log("file内容：", file.type);
                //文件分片大小
                let shardSize = 3 * 1024 * 1024;
                let shardIndex = 0.0;
                let totalIndex = Math.ceil(file.size / shardSize);
                console.log("文件大小：", file.size);
                while (shardIndex < totalIndex) {
                    let start = shardIndex * shardSize;
                    let end = Math.min(start + shardSize, file.size);
                    let formData = new window.FormData();
                    console.log("上传分片:", start, "~~~~", end);
                    //截取分片
                    let fileShard = file.slice(start, end);
                    formData.append('file', fileShard);
                    formData.append('currentIndex', shardIndex.toString());
                    formData.append('totalIndex', totalIndex.toString());
                    formData.append('fileName', file.name);
                    console.log("上传第", shardIndex, "个分片");
                    await _this.$http.post("http://localhost:9001/uploadfile", formData);
                    shardIndex++;
                }
            }
        }
    }
</script>

<style scoped>

</style>