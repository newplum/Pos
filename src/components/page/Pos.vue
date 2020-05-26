<template>
  <div class="pos">
    <el-row>
      <el-col :span="7" class="pos-order order-list">
        <el-tabs type="border-card">
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width:100%">
              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="数量" width="60"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template scope="scope">
                  <el-button type="text" size="small" @click="delSingleGoods(scope.row)">
                    删除
                  </el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">
                    添加
                  </el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="sum">
              <span>数量：{{totleCount}}</span>
              <span>金额：{{totleMoney}}元</span>
            </div>
            <div class="deal">
              <el-button type="danger" @click="delAllGoods">删除</el-button>
              <el-button type="success" @click="checkout">结账</el-button>
            </div>
          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="17">
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="goods in oftenGoods" :key="goods.goodsId" @click="addOrderList(goods)">
                <span>{{ goods.goodsName }}</span>
                <span class="price">￥{{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="goods-type">
          <el-tabs type="card">
            <el-tab-pane label="汉堡">
              <div>
                <ul class="cookList">
                  <li v-for="items in type0Goods" :key="items.goodsId" @click="addOrderList(items)">
                    <span class="foodImg">
                      <img :src="items.goodsImg" width="100%" />
                    </span>
                    <span class="foodName">{{ items.goodsName}}</span>
                    <span class="foodPrice">￥{{items.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小食">
              <ul class="cookList">
                <li v-for="items in type1Goods" :key="items.goodsId" @click="addOrderList(items)">
                  <span class="foodImg">
                    <img :src="items.goodsImg" width="100%" />
                  </span>
                  <span class="foodName">{{ items.goodsName}}</span>
                  <span class="foodPrice">￥{{items.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <ul class="cookList">
                <li v-for="items in type2Goods" :key="items.goodsId" @click="addOrderList(items)">
                  <span class="foodImg">
                    <img :src="items.goodsImg" width="100%" />
                  </span>
                  <span class="foodName">{{ items.goodsName}}</span>
                  <span class="foodPrice">￥{{items.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <ul class="cookList">
                <li v-for="items in type3Goods" :key="items.goodsId" @click="addOrderList(items)">
                  <span class="foodImg">
                    <img :src="items.goodsImg" width="100%" />
                  </span>
                  <span class="foodName">{{ items.goodsName}}</span>
                  <span class="foodPrice">￥{{items.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "pos",
  data() {
    return {
      tableData: [],
      oftenGoods: [
        {
          goodsId: 1,
          goodsName: "香辣鸡腿堡",
          price: 18
        },
        {
          goodsId: 2,
          goodsName: "田园鸡腿堡",
          price: 15
        },
        {
          goodsId: 3,
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsName: "脆皮炸鸡腿",
          price: 10
        },
        {
          goodsId: 6,
          goodsName: "魔法鸡块",
          price: 20
        },
        {
          goodsId: 7,
          goodsName: "可乐大杯",
          price: 10
        },
        {
          goodsId: 8,
          goodsName: "雪顶咖啡",
          price: 18
        },
        {
          goodsId: 9,
          goodsName: "大块鸡米花",
          price: 15
        },
        {
          goodsId: 20,
          goodsName: "香脆鸡柳",
          price: 17
        }
      ],
      type0Goods: [
        {
          goodsId: 1,
          goodsImg:
            "https://www.bkchina.cn/website/productimage/5c4024a323c39.png",
          goodsName: "香辣鸡腿堡",
          price: 18
        },
        {
          goodsId: 2,
          goodsImg:
            "https://www.bkchina.cn/website/productimage/59103e397af07.jpg",
          goodsName: "田园鸡腿堡",
          price: 15
        },
        {
          goodsId: 3,
          goodsImg:
            "https://www.bkchina.cn/website/productimage/5d54c824487e1.png",
          goodsName: "和风汉堡",
          price: 15
        }
      ],
      type1Goods: [
        {
          goodsId: 0,
          goodsImg:
            "http://www.cnhls.com/Upload/products/香酥翅-22083689682.jpg",
          goodsName: "脆皮炸鸡腿",
          price: 10
        },
        {
          goodsId: 1,
          goodsImg:
            "http://www.cnhls.com/Upload/products/心有所薯-22083693968.jpg",
          goodsName: "魔法鸡块",
          price: 20
        },
        {
          goodsId: 2,
          goodsImg:
            "http://www.cnhls.com/Upload/products/薯条20161024-22083677438.jpg",
          goodsName: "薯条",
          price: 15
        },
        {
          goodsId: 3,
          goodsImg:
            "http://www.cnhls.com/Upload/products/红豆甜心派-22083673047.jpg",
          goodsName: "红豆甜心派",
          price: 17
        }
      ],
      type2Goods: [
        {
          goodsId: 7,
          goodsImg:
            "http://www.cnhls.com/Upload/products/百事可乐-22133764786.jpg",
          goodsName: "可乐大杯",
          price: 10
        },
        {
          goodsId: 8,
          goodsImg:
            "http://www.cnhls.com/Upload/products/华莱士咖啡-22133876319.jpg",
          goodsName: "雪顶咖啡",
          price: 18
        }
      ],
      type3Goods: [
        {
          goodsId: 0,
          goodsImg:
            "https://www.bkchina.cn/website//productimage/5c36f14fc9d9c.png",
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 1,
          goodsImg: "http://www.cnhls.com/Upload/套餐E-21562719270.jpg",
          goodsName: "单人套餐",
          price: 30
        },
        {
          goodsId: 2,
          goodsImg: "http://www.cnhls.com/Upload/欢乐共享餐-21540696465.jpg",
          goodsName: "双人套餐",
          price: 50
        }
      ],
      totleMoney: 0,
      totleCount: 0,
    };
  },
  // created() {
  //   axios
  //     .get(
  //       "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods"
  //     )
  //     .then(res => {
  //       console.log("常用商品:" + res);
  //       this.oftenGoods = res.data;
  //     })
  //     .catch(err => {
  //       // console.log(err)
  //       alert("网络错误，不能访问");
  //     });
  //   axios
  //     .get(
  //       "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods"
  //     )
  //     .then(res => {
  //       console.log("商品分类:" + res);
  //       this.type0Goods = res.data[0];
  //       this.type1Goods = res.data[1];
  //       this.type2Goods = res.data[2];
  //       this.type3Goods = res.data[3];
  //     })
  //     .catch(err => {
  //       // console.log(err)
  //     });
  // },
  mounted() {
    let orderHeight = document.body.clientHeight;
    document.getElementsByClassName("order-list")[0].style.height =
      orderHeight + "px";
    this.goodsList = JSON.parse(localStorage.goodsList);
  },
  methods: {
    addOrderList(goods) {
      this.totleMoney = 0;
      this.totleCount = 0;
      //商品是否存在于订单列表中
      let isHave = false;
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsName == goods.goodsName) {
          isHave = true;
        }
      }
      //根据判断的值编写业务逻辑
      if (isHave) {
        //改变商品的数量
        let arr = this.tableData.filter(
          ele => ele.goodsName == goods.goodsName
        );
        arr[0].count++;
      } else {
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        };
        this.tableData.push(newGoods);
      }
      this.sum();
    },
    //删除单个商品
    delSingleGoods(goods) {
      if (goods.count > 1) {
        goods.count--;
      } else {
        this.tableData = this.tableData.filter(
          ele => ele.goodsId !== goods.goodsId
        );
      }
      this.sum();
    },
    //删除所有商品
    delAllGoods() {
      this.totleMoney = 0;
      this.totleCount = 0;
      this.tableData = [];
      console.log(this.goodsList)
    },
    //汇总数量和金额
    sum() {
      this.totleMoney = 0;
      this.totleCount = 0;
      if (this.tableData) {
        //计算汇总数量和金额
        this.tableData.forEach(ele => {
          this.totleCount += ele.count;
          this.totleMoney = this.totleMoney + ele.price * ele.count;
        });
      }
    },
    //模拟结账
    checkout() {
      if (this.totleCount != 0) {
        this.tableData = [];
        this.totleMoney = 0;
        this.totleCount = 0;
        this.$message({
          message: "支付成功",
          type: "success"
        });
      } else {
        this.$message.error("还未选择商品");
      }
    },
  }
};
</script>

<style scoped>
.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}
.sum {
  background-color: #fff;
  padding: 10px;
  border: 1px solid #ebeef5;
  border-top: none;
  color: #606266;
  font-size: 14px;
}
.sum span {
  margin: 0 30px;
}
.deal {
  margin-top: 10px;
  margin-left: 80px;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 10px;
  background-color: #fff;
  cursor: pointer;
}
.price {
  color: #5887ff;
}
.goods-type {
  clear: both;
}
.cookList {
  display: flex;
  flex-wrap: wrap;
}
.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  height: 62px;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  margin: 2px;
  cursor: pointer;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
}
.foodName {
  font-size: 16px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
</style>