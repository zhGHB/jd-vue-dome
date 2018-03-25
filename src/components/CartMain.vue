<template>
  <div class="shopcar" id="demo04">
    <div class="header-title">
      <h3>购物车</h3>
    </div>
    <div class="car-list">
      <ul>
        <li class="car-item" v-for="(item,index) in good_list">
          <div class="input-block">
            <label class="input-label" :class="{active: item.is_selected}" :for="'car-checkbox-'+index" @click="select_one(index)"></label>
          </div>
          <div class="car-item-content">
            <div class="car-img">
              <img :src="item.img" />
            </div>
            <div class="car-cont">
              <h3>{{item.title}}</h3>
              <div class="cat-desc">
                <span v-for="spec in item.spec_item">{{spec}}</span>
              </div>
            </div>
            <div class="num">
              <span @click="reduce(index)">-</span>
              <span>{{item.num}}</span>
              <span @click="add(index)">+</span>
            </div>
            <div class="car-price">
              <span class="car-price">￥{{item.price}}</span>
              <span class="car-num">X{{item.num}}</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <div class="car-footer">
      <div class="foot-car">
        <label for="foot-check" class="input-label" :class="{active: selected_all}" @click="slect_all"></label>
      </div>
      <div class="total-cont">
        <span>总价：{{totalPrice}}</span>
        <span>共{{totalNum}}件</span>
      </div>
      <div class="btn-box">
        <button>立即下单</button>
      </div>
    </div>
  </div>
</template>
<script type="text/javascript">
	export default {
	    data () {
	      return {
	        good_list: [
	          {
	            title: 'Apple iPhone 6s 16GB 玫瑰金色 移动联通电信4G手机',
	            img: "http://sc.tywebs.cn/public/upload/goods/2017/04-27/a767693b9a84747f25335f0e33d3d380.jpg",
	            num: 2,
	            price: 6070.00,
	            spec_item:[
	              '内存:16G',
	              '网络:4G',
	              '颜色:玫瑰金'
	            ],
	            is_selected: false
	          },{
	            title: 'Apple iPhone 6s 32GB 玫瑰金色 移动联通电信4G手机',
	            img: 'http://sc.tywebs.cn/public/upload/goods/2017/04-27/a767693b9a84747f25335f0e33d3d380.jpg',
	            num: 2,
	            price: 4570.00,
	            spec_item:[
	              '内存:32G',
	              '网络:4G',
	              '颜色:玫瑰金'
	            ],
	            is_selected: true
	          },{
	            title: 'Apple iPhone 6s 8GB 玫瑰金色 移动联通电信4G手机',
	            img: 'http://sc.tywebs.cn/public/upload/goods/2017/04-27/a767693b9a84747f25335f0e33d3d380.jpg',
	            num: 2,
	            price: 4870.00,
	            spec_item:[
	              '内存:8G',
	              '网络:4G',
	              '颜色:玫瑰金'
	            ],
	            is_selected: false
	          },{
	            title: 'Apple iPhone 6s 128GB 玫瑰金色 移动联通电信4G手机',
	            img: 'http://sc.tywebs.cn/public/upload/goods/2017/04-27/a767693b9a84747f25335f0e33d3d380.jpg',
	            num: 2,
	            price: 10568.00,
	            spec_item:[
	              '内存:128G',
	              '网络:4G',
	              '颜色:玫瑰金'
	            ],
	            is_selected: true
	          },
	        ],
	        totalPrice: 0,
	        totalNum: 0,
	        selected_all: false
	      }
	    },
	    mounted: function () {
	      this.getTotal();
	    },
	    watch: {
	      'good_list': {
	        handler: function (val, oldVal) {
	          // console.log(val)
	          return val;
	        },
	        deep: true
	      }
	    },
	    methods: {
	      getTotal () {
	        this.totalPrice = 0
	        this.totalNum = 0
	        for (var i = 0; i < this.good_list.length; i++) {
	          var _d = this.good_list[i]
	          if(_d.is_selected){
	            this.totalPrice += _d['price'] * _d['num']
	            this.totalNum +=_d['num']
	          }
	        }
	      },
	      select_one (index) {
	        if(this.good_list[index].is_selected == true){
	          this.good_list[index].is_selected = false
	        }else{
	          this.good_list[index].is_selected = true
	        }
	        this.getTotal()
	      },
	      slect_all () {
	        if(this.selected_all){
	          for (var i = 0; i < this.good_list.length; i++) {
	            this.good_list[i].is_selected = false;
	          }
	          this.selected_all = false           
	        }else{
	          for (var i = 0; i < this.good_list.length; i++) {
	            this.good_list[i].is_selected = true;
	          }
	          this.selected_all = true           
	        }
	        this.getTotal()
	      },
	      reduce (index) {
	        if(this.good_list[index].num <= 1) return;
	        this.good_list[index].num --
	        this.getTotal()
	      },
	      add (index) {
	        this.good_list[index].num ++
	        this.getTotal()
	      }
	    }
	  }
</script>
