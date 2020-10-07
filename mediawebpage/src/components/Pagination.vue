<template>
<!--  分页栏  -->
    <div>
        <nav aria-label="Page navigation">
            <ul class="pagination">
                <li @click="prePage">
                    <a href="#" aria-label="Previous">
                        <span aria-hidden="true">&laquo;</span>
                    </a>
                </li>
                <li v-for="Page in pageList" v-bind:class="{'active':currentPage===Page}" @click="alterPage(Page)">
                    <a href="#">{{Page}}</a>
                </li>
                <li @click="nextPage">
                    <a href="#" aria-label="Next">
                        <span aria-hidden="true">&raquo;</span>
                    </a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
    import {globalBus} from "./GlobalBus";

    export default {
        name: "pagination",
        data() {
            return {
                currentPage: 1,//当前页面数
                pageList: [1, 2, 3, 4, 5, 6, 7],//页面栏
                pageSize: 10//页面大小
            }
        },
        methods: {
            /**
             * 点击分页栏数字修改当前页面数
             * @param pageNumber
             */
            alterPage: function (pageNumber) {
                this.currentPage = pageNumber;
                globalBus.$emit('videoInfoCurrentPage', pageNumber);
            },
            /**
             * 上一页
             */
            prePage: function () {
                if (this.currentPage > 1) {
                    this.currentPage = this.currentPage - 1
                }
                globalBus.$emit('videoInfoCurrentPage', this.currentPage)
            },
            /**
             * 下一页
             */
            nextPage: function () {
                if (this.currentPage < 7) {
                    this.currentPage = this.currentPage + 1
                }
                globalBus.$emit('videoInfoCurrentPage', this.currentPage);
            }
        }
    }
</script>
