<template>
    <div class="often-goods">
        <div class="title">{{title}}</div>
        <div class="often-goods-list">
            <ul>
                <li v-for="item in oftenGoodsList" @click="addOrderList(item)">
                    <span>{{item.goodsName}}</span><span class="price">￥{{item.price}}元</span>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name:"oftenGoods",
        methods:{
            addOrderList(goods){
                this.$emit("addOrderList",goods);
            }
        },       
        props:['title','oftenGoodsList']
    }
</script>

<style>
.often-goods .title {
    height: 20px;
    font-size: 16px;
    text-align: left;
    padding: 10px;
    margin: 0px;
    border-bottom: 1px solid #c0ccda;
  }
  .often-goods .often-goods-list ul li {
    list-style: none;
    display: block;
    float: left;
    border: 1px solid #cccccc;
    border-radius: 5px;
    background-color: #42b983;
    padding: 10px;
    margin: 5px;
    cursor: pointer;
  }
  .often-goods .often-goods-list ul li .price {
    color: brown;
  }
</style>
