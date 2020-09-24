<template>
    <div id="video-carousel" class="carousel slide col-md-12" data-ride="carousel">
        <!-- Indicators -->
        <ol class="carousel-indicators">
            <li data-target="#video-carousel" data-slide-to="0" class="active"/>
            <li data-target="#video-carousel" data-slide-to="1"/>
            <li data-target="#video-carousel" data-slide-to="2"/>
        </ol>

        <!-- Wrapper for slides -->
        <div class="carousel-inner" role="listbox">
            <div class="item active">
                <img src="../assets/banner1.jpg" alt="../../public/xiaolan.jpg">
                <div class="carousel-caption">
                    ...
                </div>
            </div>
            <div class="item">
                <img src="../assets/banner2.jpg" alt="../../public/xiaolan.jpg">
                <div class="carousel-caption">
                    ...
                </div>
            </div>
            <div class="item">
                <img src="../assets/banner3.jpg" alt="../../public/xiaolan.jpg">
                <div class="carousel-caption">
                    ...
                </div>
            </div>
        </div>

        <!-- Controls -->
        <a class="left carousel-control" href="#video-carousel" role="button" data-slide="prev">
            <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"/>
            <span class="sr-only">Previous</span>
        </a>
        <a class="right carousel-control" href="#video-carousel" role="button" data-slide="next">
            <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"/>
            <span class="sr-only">Next</span>
        </a>
    </div>
</template>

<script>
    export default {
        name: "Carousel"
    }
</script>

<style scoped>
    .carousel-inner img{
        width: 100%;
        height: 300px;
        margin: auto;
    }
</style>