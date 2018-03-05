<template>
  <div class="hello">
    <!-- 使用element24分栏，进行栅格布局，已达到可以自动缩放适配的目的 -->
    <el-row>
      <el-col :span="9" class="pos-order" id="order-list">
        <order-list :msg="msg" :orderTableList="orderTableList" :totalCount="totalCount" :totalMoney="totalMoney" @reduceCount="reduceCount" @addOrderList="addOrderList" @accounts='accounts' @clearOrderList="clearOrderList"></order-list>
      </el-col>
      <el-col :span="15">
        <often-goods :title="title" :oftenGoodsList="oftenGoodsList" @addOrderList="addOrderList"></often-goods>
        <all-goods :staplefood="staplefood"></all-goods>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import axios from 'axios';
  import store from '@/vuex/store';
  import {
    mapState,
    mapMutations
  } from 'vuex'
  import orderList from '@/components/common/order-list'
  import oftenGoods from '@/components/common/often-goods'
    import allGoods from '@/components/common/all-goods'
  export default {
    name: "HelloWorld",
    data: function() {
      return {
        msg: "订单结算页面",
        title:"常用商品",
        orderTableList: [],
        totalCount: 0,
        totalMoney: 0,
        oftenGoodsList: [{
            goodsId: 1,
            goodsName: "香辣鸡腿堡",
            price: "16"
          },
          {
            goodsId: 2,
            goodsName: "大杯可乐",
            price: "10"
          },
          {
            goodsId: 3,
            goodsName: "大份薯条",
            price: "12"
          },
          {
            goodsId: 4,
            goodsName: "香辣鸡翅",
            price: "8"
          },
          {
            goodsId: 5,
            goodsName: "鸡米花",
            price: "11"
          },
          {
            goodsId: 6,
            goodsName: "香辣鸡块",
            price: "11"
          },
          {
            goodsId: 7,
            goodsName: "草莓圣代",
            price: "6"
          }
        ],
        staplefood:[]
      };
    },
    methods: {
      reduceCount(goods) {
        this.totalCount = 0;
        this.totalMoney = 0;
        if (goods.count == 1) {
          //从列表中移除该商品
          for (let i = 0; i < this.orderTableList.length; i++) {
            if (this.orderTableList[i].goodsName == goods.goodsName) {
              this.orderTableList.splice(i, 1);
              break;
            }
          }
        } else {
          goods.count--;
        }
        this.orderTableList.forEach(object => {
          this.totalCount += object.count;
          this.totalMoney = this.totalMoney + (object.count * object.price);
        });
      },
      addOrderList(goods) {
        // 首先判断该商品是否存在于列表中，如果存在，则数量加1，价格加上单价
        this.totalCount = 0;
        this.totalMoney = 0;
        let isHave = false;
        for (let i = 0; i < this.orderTableList.length; i++) {
          if (this.orderTableList[i].goodsName == goods.goodsName) {
            isHave = true;
            break;
          }
        }
        //如果不存在，则直接加入到列表中
        if (isHave) {
          //过滤出ID相同的
          let arr = this.orderTableList.filter(object => object.goodsName == goods.goodsName);
          arr[0].count++;
        } else {
          //构造一个新的对象，然后插入到数组当中
          let newObject = {
            goodsName: goods.goodsName,
            count: 1,
            price: goods.price
          };
          this.orderTableList.push(newObject);
        }
        this.orderTableList.forEach(object => {
          this.totalCount += object.count;
          this.totalMoney = this.totalMoney + (object.count * object.price);
        });
      },
      accounts() {
        if (this.totalCount != 0) {
          //结账
          this.$notify({
            title: "付款成功",
            message: "您已成功支付" + this.totalMoney + "元",
            type: "success",
            position: 'bottom-right',
            offset: 50
          });

          //调用vuex进行简单存储，存储之前，先对对象进行改编
          //提取当前时间
          let date=new Date();
          let currentTime=date.getFullYear()+"-"+(date.getMonth()+1)+"-"+date.getDay()+" "+date.getHours()+":"+date.getMinutes();

          let accountObject={date:currentTime,count:this.totalCount,money:this.totalMoney};
          
          this.$store.commit('addAccounts',accountObject);

          this.clearOrderList();
        }
      },
      clearOrderList() {
        this.totalCount = 0;
        this.totalMoney = 0;
        this.orderTableList = [];
      }
    },
    created() {
      axios.get("https://easy-mock.com/mock/5a7abdc0a3186d0d260d792d/example/getGoodsList").then(response => {
        console.info(response.data.data.goods);
        this.staplefood = response.data.data.goods;
      }).catch(function(error) {
        console.error(error)
      });
    },
    mounted() {
      var orderHeight = document.body.clientWidth;
      document.getElementById("order-list").style.height = orderHeight + "px";
    },
    components: {
      orderList,oftenGoods,allGoods
    },
    store
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1,
  h2 {
    font-weight: normal;
  }
  a {
    color: #42b983;
  }
  .hello {
    height: 100%;
    margin: 0px;
    padding: 0px;
  }
  .pos-order {
    background-color: #f9fafc;
    border-right: 1px solid #c0ccda;
  }
</style>
