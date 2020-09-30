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
                                <label for="InputImg">选择上传封面</label>
                                <input type="file" id="InputImg">
                            </div>
                            <div>
                                <label for="InputFile">选择上传文件</label>
                                <input type="file" id="InputFile">
                            </div>
                            <div>
                                <label for="fileDescribe">文章描述</label>
                                <textarea id="fileDescribe"/>
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
            /**
             * 1.上传图片视频至OSS
             * 2.将视频信息上传至数据库
             * @returns {Promise<void>}
             */
            async uploadFileInfo() {
                console.log("开始上传文件");
                let _this = this;
                let file = document.querySelector('#InputFile').files[0];
                let img = document.querySelector('#InputImg').files[0];
                let videoTitle=document.querySelector('#fileTitle').value;
                let videoDescribe=document.querySelector('#fileDescribe').value;
                let imgUrl =  await _this.upLoadFile2OSS(img);
                let fileUrl = await _this.upLoadFile2OSS(file);
                console.log("图片路径:",imgUrl,"视频路径:",fileUrl);
                console.log("开始给数据库传递信息");
                _this.addVideoInfo2MySQL(videoTitle,imgUrl,fileUrl,videoDescribe);
            },
            /**
             * 将文件上传到OSS的实现方法。
             * @param file：图片或者视频文件
             * @returns {Promise<string>}：文件上传至OSS对应的路径
             */
            async upLoadFile2OSS(file){
                let _this=this;
                let shardSize = 3 * 1024 * 1024;
                let shardIndex = 0.0;//视频文件分片索引
                let totalIndex = Math.ceil(file.size / shardSize);
                let fileOSSUrl='';
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
                    console.log("上传第", shardIndex, "个视频分片");
                    await _this.$http.post("http://localhost:9001/uploadfile", formData).then(function (response) {
                        console.log(response.data.fileUrl_OSS);
                        fileOSSUrl=response.data.fileUrl_OSS;
                    });
                    shardIndex++;
                }
                return fileOSSUrl;
            },
            addVideoInfo2MySQL(title,imgUrl,videoUrl,describe){
                let _this = this;
                let formData = new window.FormData();
                formData.append('title',title);
                formData.append('imgUrl',imgUrl);
                formData.append('videoUrl',videoUrl);
                formData.append('describe',describe);
                _this.$http.post("http://localhost:9001/insertVideoInfo", formData)
            }
        }
    }
</script>

<style scoped>

</style>