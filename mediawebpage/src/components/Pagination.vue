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
                currentPage: 1,
                pageList: [1, 2, 3, 4, 5, 6, 7],
                pageSize: 5
            }
        },
        methods: {
            alterPage: function (pageNumber) {
                this.currentPage = pageNumber;
                // alert("当前页面数为:"+this.currentPage);
                globalBus.$emit('userInfoCurrentPage', pageNumber);
            },
            prePage: function () {
                if (this.currentPage > 1) {
                    this.currentPage = this.currentPage - 1
                }
                globalBus.$emit('userInfoCurrentPage', this.currentPage)
            },
            nextPage: function () {
                if (this.currentPage < 7) {
                    this.currentPage = this.currentPage + 1
                }
                globalBus.$emit('userInfoCurrentPage', this.currentPage);
            }
        },
        mounted: function () {
            let _this = this;
            globalBus.$on("userInfoPageSize", function (callback) {
                _this.pageSize = callback;
            })
        },
        watch: {
            pageSize() {
                this.currentPage = 1;
            }
        }
    }
</script>
