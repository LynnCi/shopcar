<template>
    <div class="shopcar">
      <div v-if="list.length">
        <table>
          <thead>
          <tr>
            <th></th>
            <th>商品名称</th>
            <th>商品单价</th>
            <th>购买数量</th>
            <th>操作</th>
          </tr>
          </thead>
          <tbody>
            <tr v-for="(item,index) in list">
              <td>{{index+1}}</td>
              <td>{{item.name}}</td>
              <td>{{item.price}}</td>
              <td>
                <button @click="handleReduce(index)":disabled="item.count===1">-</button>
                {{item.count}}
                <button @click="handleAdd(index)">+</button>
              </td>
              <td>
                <button @click="handleRemove(index)">移除</button>
              </td>
            </tr>

          </tbody>
        </table>
        <div class="allPrices">总价：￥{{totalPrice}}元</div>
      </div>
      <div v-else>购物车为空</div>
    </div>
</template>

<script>
    export default {
      name: "shopcar",
      data(){
          return{
            list:[
              {
                id:1,
                name:'apple air',
                price:'6000',
                count:'1'
              },
              {
                id:2,
                name:'apple pro',
                price:'11000',
                count:1
              },
              {
                id:3,
                name:'applex',
                price:'7000',
                count:1
              },
              {
                id:4,
                name:'apple8',
                price:'4000',
                count:1
              },
              {
                id:5,
                name:'apple7',
                price:'3500',
                count:1
              },

            ]
          }
      },
      computed:{ //html、dom加载后执行
        totalPrice:function(){
          var total = 0;
          for(var i=0;i<this.list.length;i++){
            var item = this.list[i];
            total += item.price * item.count;
          }
          return total.toString().replace(/\B(?=(\d{3})+$)/g,',');
        }
      },
      methods:{
        handleReduce:function(index){
          if(this.list[index].count === 1){
            return;
          }
          this.list[index].count--;
        },
        handleAdd:function(index){
          this.list[index].count++;
        },
        handleRemove:function(index){
          this.list.splice(index,1);
        },
      }
    }
</script>

<style scoped>
  table{
    border:1px solid #e9e9e9;
    border-collapse: collapse;
    border-spacing:0;
    empty-cells:show;
    margin:0 auto;
  }
  th,td{
    padding:8px 16px;
    border:1px solid #e9e9e9;
    text-align:left;
  }
  th{
    background:#f7f7f7;
    color:#5c6b77;
    font-weight:600;
    white-space:nowrap;
  }
  .allPrices{
    height:40px;
    line-height: 40px;
  }

</style>
