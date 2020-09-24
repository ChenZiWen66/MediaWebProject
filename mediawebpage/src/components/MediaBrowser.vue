<template>
    <div class="media col-md-12 fff">
        <div class="media-left media-middle">
            <img id="mediaBrowserImg" class="media-object img-circle" src="../../public/xiaolan.jpg" alt="../../public/xiaolan.jpg" data-toggle="modal" data-target="#myModal" @click="$('#myModal').on('shown.bs.modal')">
        </div>
        <div class="media-body">
            <h4 class="media-heading">这是一个作品</h4>
            <p>
                富强、民主、文明、和谐、自由、平等、公正、法制、爱国、敬业、诚信、友善、
                富强、民主、文明、和谐、自由、平等、公正、法制、爱国、敬业、诚信、友善、
                富强、民主、文明、和谐、自由、平等、公正、法制、爱国、敬业、诚信、友善、
                富强、民主、文明、和谐、自由、平等、公正、法制、爱国、敬业、诚信、友善、</p>
        </div>
<!--        <MediaBrowser/>-->
    </div>
</template>

<script>
        export default {
        name: "MediaBrowser"
    }
</script>

<style scoped>
    .media img {
        width: 100px;
        height: 100px;
        margin: 5px;
    }
    .fff{
        background-color: beige;
    }
</style>