<template>
    <div class="UC_main_r">
        <div class="U_info" role="新消息">
            <div style="display: none;" class="nav_title clearfix">
                <ul class="nav_title_left">
                    <li class="icon-new-uc icon-news"></li>
                    <li>新消息 <em>12</em> 条</li>
                    <li><a href="#" class="orange">立即查看>></a></li>
                </ul>
            </div>
            <div class="U_info_content">
                <ul class="U_info_c_ul clearfix">
                    <li><h3>{{SESSIONID.user_name}} <em>，欢迎您！</em></h3></li>
                    <li>
                        <i class="font-icon">{{realGrade | limitBy 1}}</i>
                        <!--初级会员-->
                        {{realGrade}}
                    </li>
                    <li><a v-link="{path:'/u/exchange/cashing'}">
                        积分：<em class="orange">{{SESSIONID.total_jifen}}</em></a>
                    </li>
                    <li>
                        <a v-link="{path:'/u/exchange/rule'}"  class="orange">积分规则>></a>
                    </li>
                    <div class="U_info_c_setting">
                        <a href="javascript:;;">常用信息设置 <i role="三角形" class="arrow-down"></i></a>
                        <ul class="U_info_c_ul_setting">
                            <li><a v-link="{path:'/u/accout/info'}">基本资料</a> </li>
                            <li><a v-link="{path:'/u/accout/address'}">地址管理</a></li>
                            <li><a v-link="{path:'/u/accout/head'}">头像管理</a></li>
                            <li><a v-link="{path:'/u/accout/modify'}">修改密码</a></li>
                        </ul>
                    </div>
                </ul>
                <ul class="U_info_c_ul u_info_order clearfix">
                    <li><a v-link="{path:'/u/order/payment'}">已付定金<em class="orange">&nbsp;&nbsp;{{baseinfo.deposit}}</em></a></li>
                    <li>|</li>
                    <li><a v-link="{path:'/u/order/liftCar'}">待提车<em class="orange">&nbsp;&nbsp;{{baseinfo.mentioncars}}</em></a></li>
                    <li>|</li>
                    <li><a v-link="{path:'/u/order/shipment'}">出库中<em class="orange">&nbsp;&nbsp;{{baseinfo.library}}</em></a></li>
                </ul>
            </div>
        </div>
        <div class="U_new_order" role="订单表">
            <div class="nav_title clearfix">
                <ul class="nav_title_left">
                    <li class="nav_title_li_border"></li>
                    <li><strong>最新订单</strong></li>
                </ul>
                <div class="nav_title_right">
                    <a v-link="{path:'/u/order/all'}">查看订单</a>
                </div>
            </div>
            <div class="U_info_content">
                <div class="table">
                    <table>
                        <thead>
                        <tr>
                            <th class="common_name">商品</th>
                            <th class="common_low_price">总价/元</th>
                            <th class="common_money">定金/元</th>
                            <th class="common_status">交易状态</th>
                            <th class="common_buy_time">提车时间</th>
                            <th class="common_info">买家信息</th>
                        </tr>
                        </thead>
                    </table>
                </div>
                <div class="table">
                    <table>
                        <thead v-if="!istrue">
                            <tr>
                                <th colspan="6">
                                    <p v-if="neworder!=null"  class="order">
                                        下单时间：<span>{{neworder.createtime}} </span>订单号：<span>{{neworder.out_trade_no}}</span>
                                    </p>
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-if="istrue">
                                <td colspan="6" style="text-align: center; font-size: 16px;">
                                    <div class="order-nodata">
                                        <h4><i class="order-nobg"></i>抱歉，暂无相关信息！</h4>
                                        <p>您可进入 <a v-link="{ path:'/u/order/all'}">购车订单</a> 页面更新底价信息</p>
                                    </div>
                                </td>
                            </tr>
                            <tr v-if="!istrue">
                                <td class="common_name">
                                    <dl class="clearfix">
                                        <dt>
                                            <img v-bind:src="neworder.exterior_img" alt="" width="120" height="80">
                                        </dt>
                                        <dd style="width: 218px;">
                                            <a class="orange">{{neworder.carstyle}}</a>
                                            <p>外观：{{neworder.interior_color_name}}  内饰：{{neworder.exterior_color_name}}</p>
                                        </dd>
                                    </dl>
                                </td>
                                <td class="common_low_price">
                                    {{neworder.low_price}}
                                </td>
                                <td class="common_money">
                                    {{neworder.money}}
                                </td>
                                <td class="common_status">
                                    <p v-if="neworder.status==0">未支付</p>
                                    <p v-if="neworder.status==1">已支付（未完善）</p>
                                    <p v-if="neworder.status==2">已失效</p>
                                    <p v-if="neworder.status==3">审核中</p>
                                    <p v-if="neworder.status==4">通过审核</p>
                                    <p v-if="neworder.status==5">未通过审核</p>
                                    <p v-if="neworder.status==6">出库中</p>
                                    <p v-if="neworder.status==7">提车中</p>
                                    <p v-if="neworder.status==8">已完成</p>
                                    <p v-if="neworder.status==9">支付中</p>
                                    <p v-if="neworder.status==10">支付失败</p>
                                    <!--<a v-link="" style="color:#48a6fc;">订单详情</a>-->
                                </td>
                                <td class="common_buy_time">
                                    {{neworder.buy_time}}
                                </td>
                                <td class="common_info">
                                    <p>姓名：{{neworder.buyer_name}}</p>
                                    <p>手机：{{neworder.buyer_tel}}</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                    {{sum}}
                </div>
            </div>
        </div>
        <div class="U_new_eye" role="报价">
            <div class="nav_title clearfix">
                <ul class="nav_title_left">
                    <i role="icon"></i>
                    <li class="nav_title_li_border"></li>
                    <li><strong>最新报价</strong></li>
                </ul>
                <div class="nav_title_right">
                    <a v-link="{path:'/u/manage/myOffer/find/0'}">报价管理</a>
                </div>
            </div>
            <div class="U_info_content">
                <offer-table :stats="stats" :judge="judge" :idx="idx" :explain="explain" :pagesize="1"  :arr_area_offer="arr_area_offer" :arr_offer="arr_offer"></offer-table>
            </div>
        </div>
        <div class="U_new_active" role="活动">
            <div class="nav_title clearfix">
                <ul class="nav_title_left">
                    <li class="nav_title_li_border"></li>
                    <li><strong>最新活动</strong></li>
                </ul>
                <div class="nav_title_right">
                    <a v-link="{path:'/u/active/thisShop/find/0'}">活动车款</a>
                </div>
            </div>
            <div class="U_info_content">
                <active-table :stats="stats" :judge="judge" :idx="idx" :explain="explain" :pagesize="1"  :arr_area_active="arr_area_active" :arr_active="arr_active"></active-table>
            </div>
        </div>
        <div class="U_new_integral" role="积分兑换">
            <div class="nav_title clearfix">
                <ul class="nav_title_left">
                    <li class="nav_title_li_border"></li>
                    <li><strong>积分兑换</strong></li>
                    <li><a v-link="{path:'/u/exchange/cashing'}">前往兑换</a></li>
                </ul>
                <!--<div class="nav_title_right">

                </div>-->
            </div>
            <div class="U_info_content">
                <div class="carousel">
                    <button class="left" v-on:click="pre()" role="上一页"><</button>
                    <div class="carousel_div">
                        <ul class="arousel_ul clearfix">
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-1.jpg">
                                        <p class="G_fl">积分：<span>400</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-2.jpg">
                                        <p class="G_fl">积分：<span>400</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-3.jpg">
                                        <p class="G_fl">积分：<span>400</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-4.jpg">
                                        <p class="G_fl">积分：<span>400</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-5.jpg">
                                        <p class="G_fl">积分：<span>2000</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-6.jpg">
                                        <p class="G_fl">积分：<span>3800</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-7.jpg">
                                        <p class="G_fl">积分：<span>6500</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                            <li v-on:click="goCashing">
                                <div class="gift-left-box G_fl">
                                    <div class="num_full clearfix">
                                        <img src="../assets/img/gift-8.jpg">
                                        <p class="G_fl">积分：<span>7000</span></p>
                                        <p class="G_fl">数量：<span>充足</span></p>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                    <button class="right" v-on:click="next()" role="下一页">></button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import NavPagination from '../components/NavPagination.vue'
    import OfferTable from  '../components/4shome/OfferTable.vue'
    import ActiveTable from '../components/4shome/ActiveTable.vue'
    import $ from 'jquery'
    import config from './../config'
    import util from './../util/util'
    export default {
        route:{
            data({to,next}){
                this.SESSIONID = JSON.parse(sessionStorage.getItem("SESSIONID")) ;
				
                var that = this;
                var params = {"query":{"user_id":config.USERID()}};
                $.ajax({
                    url:config.API_BASE+"/4s/home/index",
                    method:"POST",
                    contentType: 'application/json; charset=utf-8',
                    dataType:"json",
                    data:JSON.stringify(params),
                    beforeSend:function (request) {
                        request.setRequestHeader("sessionid",config.SESSIONID());
                    },
                    success:function (response) {
//                        layer.close(ii);
                        if(response.code==0){
                            var data = response.data;
                            that.baseinfo = data.baseinfo;
                            that.neworder = data.neworder;
                            that.istrue = $.isEmptyObject(that.neworder);
                            that.$set("arr_active",data.newactivity);
                            that.arr_area_active = data.pricearea;
                            that.$set("arr_offer",data.newprice);
                            that.arr_area_offer = data.specialpricearea;
                            that.grade = data.grade;
                        }
                    },
                    error:function (fail) {
                        if(fail.status == "401"){
                            var SESSIONID = sessionStorage.getItem("SESSIONID");
                            if(SESSIONID == null){
                                that.$route.router.go("/login");
                            }else{
                                sessionStorage.removeItem("SESSIONID");
                                layer.msg('登录失效，请重新登陆！');
                                util.login();
                            }
                        }
                    }
                });
                next();
            }
        },
        ready(){
            this.c_width= $(".carousel_div").width();
            $(".UC_nav").find('a').removeClass("active").find("i").removeClass("i_active_1 i_active_2 i_active_3 i_active_4 i_active_5 i_active_6 i_active_0");
            $(".UC_nav").find('li').eq(0).find('a').addClass("active").find("i").addClass("i_active_0");
        },
        computed: {
            sum: function() {
                var obj = this.neworder;
                this.istrue = $.isEmptyObject(obj);
                return ;
            },
            realGrade(){
                // 等级分类
            	this.SESSIONID = JSON.parse(sessionStorage.getItem("SESSIONID")) ;
                if(this.SESSIONID!=null||this.SESSIONID!=undefined){
                    var grade = this.SESSIONID.total_jifen;

                    if(grade < 5000){
                        return "初级会员";
                    }else if(grade <= 10000){
                        return "中级会员";
                    }else if(grade > 10000){
                        return "高级会员";
                    }else{
                        return "无";
                    }
                }
	        }
        },
        data(){
            return {
                stats:1,
                judge:true,
                idx:'4',
                explain:"如您对官方价有疑问，请致电400-138-0808。",
                arr_area_offer:[],
                arr_area_active:[],
                arr_offer:{},
                arr_active:{},
                c_width:'',
                cur:0,
                c_sum:2,
                SESSIONID:{},
                baseinfo:[],
                neworder:{},
                istrue:"",
                grade:1
            }
        },
        components:{
            NavPagination,
            OfferTable,
            ActiveTable
        },
        methods:{
            pre(){
                if(this.cur <=0){
                    return;
                }
                this.cur--;
                $(".arousel_ul").animate({"left":"-"+this.cur*this.c_width+"px"},1500);
            },
            next(){
                if(this.cur >=2){
                    return;
                }
                this.cur++;
                $(".arousel_ul").animate({"left":"-"+this.cur*this.c_width+"px"},1500);
            },
            goCashing(){
                this.$route.router.go("/u/exchange/cashing");
            }
        }
    }
</script>

<style scoped>
    .active{
        color: orange;
    }

    .UC_main_r {
        width: 100%;
        display: inline-block;
        letter-spacing: normal;
        word-spacing: normal;
        vertical-align: top;
        font-size: 12px;
        /*min-height: 600px;*/
        padding-bottom: 0px!important;
    }
    /*store*/
    .nav_title{
        margin:10px 0 0 0;
    }
    .nav_title .nav_title_left {
        float: left;
        margin-left: 20px;
        padding: 10px;
        display: inline-block;
        width: 50%;
    }
    .nav_title .nav_title_left li {
        float: left;
        padding-left: 5px;
        margin: 0;
        display: inline-block;
    }
    .nav_title .nav_title_left .nav_title_li_border {
        border-left: 4px solid #ff7920;
        height: 17px;
    }
    .nav_title .nav_title_left .icon-news {
        background-position: -60px -290px;
    }
    .nav_title .nav_title_left em {
        color: #ff7920;
    }
    .nav_title .nav_title_right {
        float: right;
        display: inline-block;
        padding: 10px;
        margin-right: 30px;
    }
    .U_info{
        margin-top: 30px;
    }
    .U_info_content {
        width: 94%;
        margin: 0 auto;
        color: #999;
    }
    .U_info_content .U_info_c_ul {
        position: relative;
        padding: 10px;
        border: 1px solid #ccc;
        background: #f7f7f7;
    }

    .U_info_content .u_info_order{
        border-top: none;
        background: #FFF;
    }
    .U_info_content .u_info_order li{
        margin: 0 60px!important;
    }
    i.font-icon{
        display: inline-block;
        width: 20px;
        height: 20px;
        border-radius: 4px;
        background: #ff791f;
        color: #FFFFFF;
        /*vertical-align: middle;*/
        line-height: 18px;
        font-style: normal;
        text-align: center;
        overflow: hidden;
        vertical-align: top;
    	margin-top: 5px;
    }
    .U_info_content .U_info_c_ul li {
        float: left;
        line-height: 30px;
        margin: 0 20px;
    }
    .U_info_content .U_info_c_ul li h3{
        font-size: 18px;
        color: #343434;
    }
    .U_info_content .U_info_c_ul li h3 em{
        font-size: 14px;
    }
    .U_info_content .U_info_c_setting{
        float: right;
        margin-right: 10px;
        padding: 10px 15px;
        position: absolute;
        width: 90px;
        right: 0;
        z-index: 9;
        cursor: pointer;
    }
    .U_info_content .U_info_c_setting:hover{
        padding: 9px 14px;
        border: 1px solid #e6e6e6;
        background: #FFF;
    }
    .U_info_content .U_info_c_setting a{
        position: relative;
        display: block;
    }
    .U_info_content .U_info_c_setting a > i{
        position: absolute;
        bottom: 5px;
        right: -4px;
    }
    .U_info_content  .U_info_c_setting .U_info_c_ul_setting{
        display: none;
    }
    .U_info_content .U_info_c_setting:hover > .U_info_c_ul_setting{
        display: block;
    }

    .U_info_content  .U_info_c_setting .U_info_c_ul_setting li{
        float: none;
    }
    .U_info_content  .U_info_c_setting .U_info_c_ul_setting li a:hover{
        color: #ff791f;
    }
    .orange {
        color: #ff7920;
    }
    /*new order*/
    table{
        width: 100%;
        border:1px solid #ccc;
    }
    table thead tr th{
        padding: 10px 0;
        text-align: center;
        background: #f1f2f3;
        color: #000000;
    }
    table tbody tr td{
        border: 1px solid #ccc;
        text-align: center;
        /*padding: 20px 5px;*/
    }
    table tbody tr td dl dd,table tbody tr td dl dt{
        float: left;
    }
    table tbody tr td dl dd{
        line-height: 30px;
        margin-top: 20px;
    }
    table tbody tr td dl dd a{
        line-height: normal;
    }
    table tbody tr td a {
        display: block;
    }
    table .common_name{
        width: 350px;
    }
    table .common_low_price{
        width: 90px;
    }
    table .common_money{
        width: 90px;
    }
    table .common_status{
        width: 90px;
    }
    table .common_buy_time{
        width: 120px;
    }
    table .common_info{
        width: 145px;
    }
    table .order{
        color: #999;;
        text-align: left;
        margin-left: 15px;
    }
    table .order span{
        color: #666;
    }
    .carousel{
        position: relative;
        margin-bottom: 50px;
    }
    .carousel_div{
        width: 800px;
        overflow: hidden;
        margin: 0 auto;
    }
    .carousel ul{
        position: relative;
        width: 5400px;
        height: 160px;
        margin: 0 auto;
    }
    .carousel ul > li {
        float: left;
        margin-right: 22px;
        cursor:pointer;
    }
    .carousel button{
        position: absolute;
        display: inline-block;
        width: 30px;
        height: 60px;
        font-size: 18px;
        color: #FFFFFF;
        background: rgba(0, 0, 0, 0.5);
        border: none;
        cursor: pointer;
        z-index: 8;
    }
    .left{
        top: 25%;
        left: -10px;
    }
    .right{
        top: 25%;
        right: 8px;
    }
    .gift-left-box {
        margin-left: 0!important;
        margin-bottom: 30px;
    }
    .num_full {
        background: #f0f0f0;
        width: 246px;
    }
    .num_full img{
        width: 100%;
    }
    .num_full p {
        width: 45%;
        margin-left: 10px;
    }
    .G_fl {
        float: left;
        _display: inline;
    }
	.order-nodata{
		border: none;
	}
    .order-nodata h4{
        color: #4c4c4c;
        font-size: 18px;
        line-height: 46px;
    }
    .order-nodata p a{
        display: inline-block;
        color: #2194fe;
    }
    .order-nodata .order-nobg{
        width: 30px;
        height: 30px;
        display: inline-block;
        vertical-align: top;
        margin-top: 8px;
        margin-right: 8px;
        background-image: url('./../assets/img/ico_warn.png');
        background-repeat: no-repeat;
        background-position: -82px 4px;
        background-size: 300px 150px;
    }
</style>
