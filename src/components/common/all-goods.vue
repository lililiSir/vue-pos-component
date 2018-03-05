<template>
    <div class="all-goods">
        <div class="title">所有商品</div>
        <div class="all-goods-list">
            <el-tabs v-model="goodsTabName" style="margin-left:10px">
                <el-tab-pane label="主食" name="first">
                    <div class="staplefood">
                        <ul>
                            <li v-for="item in staplefood">
                                <span class="foodImg"><img :src='item.goodsUrl' width="64" height="64"/></span>
                                <span class="foodName">{{item.goodsName}}</span>
                                <span class="foodPrice" style="">￥{{item.goodsPrice}}元</span>
                            </li>
                        </ul>
                    </div>
                </el-tab-pane>
                <el-tab-pane label="小食" name="second">小食</el-tab-pane>
                <el-tab-pane label="饮料" name="third">饮料</el-tab-pane>
                <el-tab-pane label="套餐" name="fouth">套餐</el-tab-pane>
            </el-tabs>
        </div>
    </div>
</template>

<script>
    export default {
        name:"allGoods",
        data(){
            return {
                goodsTabName:"first"
            }
        },
        props:["staplefood"]
    }
</script>

<style>
    .all-goods {
        margin-top: 150px;
        clear: both;
    }
    .all-goods .title {
        height: 20px;
        font-size: 16px;
        text-align: left;
        padding: 10px;
        margin: 0px;
        border-bottom: 1px solid #c0ccda;
    }
    .staplefood ul li {
        list-style: none;
        display: block;
        float: left;
        border: 1px solid #cccccc;
        border-radius: 5px;
        background-color: #42b983;
        padding: 8px;
        margin: 5px;
        cursor: pointer;
    }
    .staplefood .foodImg {
        float: left;
    }
    .staplefood .foodName {
        display: block;
        float: left;
        padding: 10px;
    }
    .staplefood .foodPrice {
        display: block;
        margin-top: 40px
    }
</style>
