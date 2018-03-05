<template>
    <div class="orderList">
        <h2>{{msg}}</h2>
        <el-tabs v-model="acitveName" style="margin-left:10px">
            <el-tab-pane label="点单" name='first'>
                <el-table :data="orderTableList" stripe border fit style="width:100%;" align="center">
                    <el-table-column prop="goodsName" label="商品" align="center"></el-table-column>
                    <el-table-column prop="count" label="数量" align="center"></el-table-column>
                    <el-table-column prop="price" label="金额" align="center"></el-table-column>
                    <el-table-column label="操作" align="center" fixed="right">
                        <template slot-scope="scope">
                      <el-button size="mini" type="text" @click="reduceCount(scope.row)">删除</el-button>
                      <el-button size="mini" type="text" @click="addOrderList(scope.row)">增加</el-button>
                        </template>
              </el-table-column>
            </el-table>
            <div class="totalDiv" style="text-align:left">
              <div>
                <span>数量：{{totalCount}} 件 &nbsp;&nbsp;&nbsp; 金额：{{totalMoney}} 元</span>
              </div>
            </div>
            <div style="margin-top:10px">
              <el-button size="mini" type="primary" @click="accounts">结账</el-button>
              <el-button size="mini" type="danger" @click="clearOrderList">清空</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单" name='second'>挂单</el-tab-pane>
          <el-tab-pane label="外卖" name='third'>外卖</el-tab-pane>
        </el-tabs>
  </div>
</template>

<script>
    export default {
        name: "orderList",
        data() {
            return {
                acitveName: "first"
            };
        },
        methods: {
            reduceCount(goods) {
                this.$emit("reduceCount",goods);
            },
            addOrderList(goods) {
                this.$emit("addOrderList",goods);
            },
            accounts() {
                this.$emit("accounts");
            },
            clearOrderList() {
                this.$emit("clearOrderList");
            }
        },
        props: ['msg',"orderTableList", "totalCount", "totalMoney"]
    };
</script>

<style>

</style>
