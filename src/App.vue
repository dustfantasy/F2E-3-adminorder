<template>
  <div id="app">
    <header>
      <div class="left">
         Shoptime
      </div>
      <div class="center">
        <div class="active">HOME</div>
        <div>ORDERS</div>
        <div>PRODUCT</div>
      </div>
      <div class="right">
        ADMIN
      </div>      
    </header>
    <main>
      <div class="left">OVERVIEW</div>
      <div class="right">
        2018/6/6 <i class="fas fa-caret-right"></i>2018/6/13　
        Weekly<i class="fas fa-caret-down"></i>
      </div>
      <div class="overview">
        
        <div class="revenue">
          <div>TOTAL revenue</div>
          <span class="count">54540</span>
        </div>
        <div class="cost">
          <div>TOTAL COST</div>
          <span class="count">12660</span>
        </div>
        <div class="income">
          <div>NET INCOME</div>
          <span class="count">41880</span>
        </div>
        
        <div class="activity">
          <div class="title">Activity</div>
          <div id="chart-line"></div>
        </div>
        
        <div class="web">
          <div class="title">Transaction Website</div>
          <div class="weblist">
            <div :class="{list:true, border: web !== 1}" v-for="web in weblist" :key="'w' + web">
              <div class="img">
                <img src="@/assets/fb.svg">
              </div>
              <div class="url">Facebook.com</div>
              <div class="count">45,836</div>
              <div class="persent">
                <span class="up" v-show="web === 1">20%</span>
                <span class="down" v-show="web !== 1">20%</span>
              </div>
            </div>
          </div>
        </div>
        <div class="order">
          <div class="title">Latest Orders</div>
          <div class="orderlist">
            <div :class="{list:true, border: order !== 1}" v-for="order in orderlist" :key="'o' + order">
              <div class="img">
                <img src="@/assets/product.jpeg">
              </div>
              <div class="product">
                <div class="title">Vintage T-shirt</div>
                <div class="time">2018/6/13  13:42</div>
                <div class="person">Belle Willis</div>
              </div>
              <div class="total">
                <p>Total</p>
                <span>1,600</span>
              </div>
            </div>
          </div>
        </div>
        
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function(){
    return {
      weblist: [1,2,3,4],
      orderlist: [1,2,3]
    }
  },
  mounted() {
    this.chartLine()
  },
  methods: {
    chartLine() {
      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);

      function drawChart() {
        var data = google.visualization.arrayToDataTable([
          ['Date', 'revenue', 'cost', 'income'],
          ['6 JUN',  7200,      400 ,  5000],
          ['7 JUN',  1170,      4600,  2000],
          ['8 JUN',  5000,      1120,  3500],
          ['9 JUN',  1030,      5400,  4000]
        ]);

        var options = {
          legend: { position: 'none' },
          width: 1154,
          height: 310
        };

        var chart = new google.visualization.LineChart(document.getElementById('chart-line'));

        chart.draw(data, options);
      
      }
    }
  }
}
</script>

<style lang="sass">
$headerH: 70px;
$green: #7ED321;
$red: #D0021B;
$blue: #4A90E2;
@mixin page-padding 
	padding: 0px 30px;
@mixin title
  font-weight: bold
  color: #000000; 
  font-size: 24px;
@mixin total-area($color, $area)
  font-weight: bold
  font-size: 16px;
  color: #000000; 
  padding: 26px 70px
  height: 138px
  grid-area: $area
  background-color: #fff
  div
    &:before
      font-family: FontAwesome
      content: "\f155"
      margin-right: 10px
  .count
    font-size: 36px;
    color: $color


html 
  height: 100%;
  body 
    margin: 0px 0px;
    height: 100%;
    background: #F2F2F2 ;

#app 
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;

  header
    +page-padding
    display: inline-block;
    width: 100%;
    background-color: #000;
    color: #fff;
    font-weight: bold;
    .left
      text-align: left;
      font-size: 24px;
      line-height: $headerH;
      display: inline-block;
      width: 200px;
      height: $headerH;
      vertical-align: top;
    .right
      text-align: right;
      font-size: 16px;
      line-height: $headerH;
      display: inline-block;
      width: 200px;
      height: $headerH; 
      vertical-align: top;
    .center
      display: inline-block;
      width: calc(100% - 410px);      
      height: $headerH;
      vertical-align: top;
      text-align: left;
      
      > div
        display: inline-block;
        width: auto;
        height: $headerH;
        padding: 0px 20px;
        text-align: center;
        line-height: $headerH;
        font-size: 16px;
        color: #9B9B9B;
        &.active
          border-bottom: 4px solid #fff;
          color: #fff;
  main
    +page-padding
    padding: 30px
    overflow: auto
    .left
      float: left;
      text-align: left;
      +title
    .right
      float: right;
      font-size: 16px;
      color: #9B9B9B;
      text-align: right;
      .fa-caret-right
        color: #000
        margin: 0px 5px
      .fa-caret-down
        color: #000
        margin-left: 10px
    .overview
      float: left
      clear: both
      margin-top: 20px
      width: 100%
      display: grid
      grid-template: "revenue revenue cost cost income income" auto "activity activity activity activity activity activity" auto "web web web order order order" auto
      grid-gap: 20px
      .revenue
        +total-area($green, revenue)
      .cost
        +total-area($red, cost)      
      .income
        +total-area($blue, income)
      .activity
        height: 406px
        grid-area: activity
        padding: 30px 40px
        background-color: #fff
        .title
          text-align: left
          +title
        #chart-line
          width: 100%
          height: calc(100% - 36px)
      .web
        height: 456px
        grid-area: web
        padding: 30px 40px
        background-color: #fff
        .title
          text-align: left
          +title
        .weblist
          height: calc(100% - 36px)
          display: grid
          grid-template-columns: 1fr
          .border
            border-top: 1px solid #EBEBEB
          .list
            display: grid
            grid-template: "img url count persent" / 1fr 3fr 2fr 80px
            grid-gap: 10px 10px
            .img
              grid-area: img
              display: inline-grid
              justify-content: center
              align-items: center
              img
                height: 45px
                width: 45px
            .url
              grid-area: url
              display: inline-grid
              align-items: center
              font-size: 16px;
              color: #9B9B9B;
              text-align: left;
            .count
              grid-area: count
              display: inline-grid
              align-items: center
              font-size: 20px;
              color: #000000;
              text-align: right;
            .persent
              grid-area: persent
              display: inline-grid
              align-items: center
              font-size: 16px;
              text-align: center;
              .up:before
                color: $green;
                margin-right: 5px
                font-family: FontAwesome
                content: '\f062'
              .down:before
                color: $red;
                margin-right: 5px
                font-family: FontAwesome
                content: '\f063'
          
      .order
        height: 456px
        grid-area: order
        padding: 30px 40px
        background-color: #fff
        .title
          text-align: left
          +title
        .orderlist
          height: calc(100% - 36px)
          display: grid
          grid-template-columns: 1fr
          .border
            border-top: 1px solid #EBEBEB
          .list
            display: grid
            grid-template: "img product total" / 1fr 3fr 1fr
            grid-gap: 5px 10px
            .img
              grid-area: img
              display: inline-grid
              justify-content: center
              align-items: center
              img
                height: 100px
                width: 100px
            .product
              padding: 20px 0px
              grid-area: product
              display: inline-grid
              grid-gap: 0px 0px
              align-items: center
              font-size: 16px;
              color: #9B9B9B;
              text-align: left;
              .title
                +title
              .time:before
                display: inline-block
                width: 20px
                text-align: center
                font-family: FontAwesome
                content: '\f017'
              .person:before
                display: inline-block
                width: 20px
                text-align: center
                font-family: FontAwesome
                content: '\f183'
            .total
              padding: 20px 0px
              grid-area: total
              display: inline-grid
              grid-template: 1fr / 1fr
              align-items: flex-end
              font-size: 20px
              color: #000000
              text-align: right
              > p
                font-size: 14px
              > span
                +title

</style>
