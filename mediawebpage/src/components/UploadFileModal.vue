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
            async uploadFileInfo() {
                /**
                 * 1.上传文件
                 * 2.在表单中添加信息
                 * 3.访问接口http://localhost:9001/uploadfile
                 */
                console.log("开始上传文件");
                let _this = this;
                let file = document.querySelector('#InputFile').files[0];
                let img = document.querySelector('#InputImg').files[0];
                let videoTitle=document.querySelector('#fileTitle').value;
                let videoDescribe=document.querySelector('#fileDescribe').value;
                // let shardSize = 3 * 1024 * 1024;
                // let imgShardIndex=0.0;//图片分片索引
                // let imgTotalIndex=Math.ceil(img.size / shardSize);//图片最大分片索引
                // let shardIndex = 0.0;//视频文件分片索引
                // let totalIndex = Math.ceil(file.size / shardSize);//视频最大分片索引
                // console.log("开始上传封面图片");
                // while(imgShardIndex<imgTotalIndex){
                //     let imgStart=imgShardIndex*shardSize;
                //     let imgEnd = Math.min(imgStart + shardSize, img.size);
                //     let ImgFormData = new window.FormData();
                //     console.log("上传分片:", imgStart, "~~~~", imgEnd);
                //     //截取分片
                //     let ImgShard = img.slice(imgStart, imgEnd);
                //     ImgFormData.append('file', ImgShard);
                //     ImgFormData.append('currentIndex', shardIndex.toString());
                //     ImgFormData.append('totalIndex', totalIndex.toString());
                //     ImgFormData.append('fileName', img.name);
                //     console.log("上传第", shardIndex, "个图片分片");
                //     await _this.$http.post("http://localhost:9001/uploadfile", ImgFormData);
                //     shardIndex++;
                // }
                // console.log("开始上传视频");
                // while (shardIndex < totalIndex) {
                //     let start = shardIndex * shardSize;
                //     let end = Math.min(start + shardSize, file.size);
                //     let formData = new window.FormData();
                //     console.log("上传分片:", start, "~~~~", end);
                //     //截取分片
                //     let fileShard = file.slice(start, end);
                //     formData.append('file', fileShard);
                //     formData.append('currentIndex', shardIndex.toString());
                //     formData.append('totalIndex', totalIndex.toString());
                //     formData.append('fileName', file.name);
                //     console.log("上传第", shardIndex, "个视频分片");
                //     await _this.$http.post("http://localhost:9001/uploadfile", formData).then(function (response) {
                //         console.log(response.data.fileUrl_OSS);
                //     });
                //     shardIndex++;
                // }
                let imgUrl =  await _this.upLoadFile2OSS(img);
                let fileUrl = await _this.upLoadFile2OSS(file);
                console.log("图片路径:",imgUrl,"视频路径:",fileUrl);
            },
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
            }
        }
    }
</script>

<style scoped>

</style>