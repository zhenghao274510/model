<template>
  <div class="box">
    <img class="bg" src="@/assets/images/bg.png" alt="">
    <div class="top">
      <img :src="dataobject.usericon" class="avtor" alt="">
      <span class="s1">关注</span>
      <p class="pcom">{{dataobject.username}}</p>
      <ul class="ut">
        <li>{{dataobject.useraddress}}</li>
        <li>芝麻分:{{dataobject.userzhima}}</li>
        <li>关注:{{dataobject.userguanzhu}}</li>
        <li>粉丝:{{dataobject.userfensi}}</li>
      </ul>
    </div>
    <van-tabs v-model="active" title-active-color="#2076FF" color="#2076FF" :border="false">
      <van-tab title="详情">
        <div class="line"></div>
        <div class="con">
          <p class="p1">
            <span class="corg">{{dataobject.classname}}</span> 
            <span>{{dataobject.name}}</span>             
          </p>
          <ul class="ul1">
            <li class="first">成交量：{{dataobject.salecount}}</li><li class="starpricre"> <span class="corg">￥{{dataobject.money}}</span> 元起</li>
            <li style="flex-grow:1;text-align:right;color:#999;">{{dataobject.looknum}}人浏览</li>
          </ul>
          <p class="pw">
              {{dataobject.worktime}}  
          </p>
          <p class="p1">技能详情</p>
          <p class="p3">{{dataobject.content}}</p>
          <div class="detail">
            <img src="@/assets/images/banner.jpg" alt="">            
          </div>
          <p class="p1">案例</p>
          <div class="detail" v-for="(item,index) in dataobject.caseList" :key="index">
            <p class="p3">{{dataobject.casecontent}}</p>
            <img :src="i" alt="" v-for="i in item.caseimage" :key="i">            
          </div>
          <p  class="corg" style="line-height:20px;font-size:11px;">              
            注：凡是要求缴纳定金及保证金的都涉嫌诈骗，为了您的财务安全请走线上交易
          </p>
        </div>
      </van-tab>
      <van-tab title="评价" disabled>
        <div class="line"></div>
      </van-tab>
      <van-tab title="店铺" disabled>
        <div class="line"></div>
      </van-tab>
    </van-tabs>
    <div class="line"></div>
    <div class="con2">
      <p class="liuptitle">
        <span class="bold">留言 (3)</span>       
      </p>
      <section class="liuycontent">
        <ul>
           <!-- <li v-for="(item,index) in dataList" :key="index">
            <div class="topflex">
                <div>
                  <img src="@/assets/images/touxiang.png" alt="" class="lyavator">
                  <span class="c333">专职愉公</span>
                </div>
                <span class="c9">1楼</span>
            </div>
            <div class="middle">
              怎么做？怎么做？怎么做？怎么做？做？怎么做？怎么做？怎么做？怎么做？怎么做？怎么做？
            </div>
            <div class="bottom">
              <div class="time">
                2019-05-09  11：32：25
              </div>
              <div class="option">
                <img src="@/assets/images/news.png" alt="" class="icon">
                <span>回复</span>
                <img src="@/assets/images/zan.png" alt="" class="icon">
                <span>0</span>
              </div>
            </div>
          </li> -->
          <li v-for="(item,index) in dataList" :key="index">
            <div class="topflex">
                <div>
                  <img :src="item.usericon" alt="" class="lyavator">
                  <span class="c333">{{item.username}}</span>
                </div>
                <span class="c9">{{index+1}}楼</span>
            </div>
            <div class="middle">
             {{item.content}}
            </div>
            <div class="bottom">
              <div class="time">
                {{item.time}}
              </div>
              <div class="option">
                <img src="@/assets/images/news.png" alt="" class="icon">
                <span>回复</span>
                <img src="@/assets/images/zan.png" alt="" class="icon" v-if="item.iszan==0">
                <img src="@/assets/images/zan2.png" alt="" class="icon" v-if="item.iszan==1">
                <span>{{item.zancount}}</span>
              </div>            
            </div>
            <div class="replay" v-if="item.secondcount!=0">
              <p><span class="respan"> @{{item.username}}：</span><span class="c666"> 先报名！</span></p>
              <p class="more">共{{item.secondcount}}条回复></p>
            </div>
          </li>
        </ul>
      </section>
    </div>
    <div class="btmbar" v-if="!isscroll">
      <ul>
        <li class="bg0">留言</li>
        <li class="bg1">举报</li>
        <li class="bg2">报名</li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  components: {  },
  data() {
    return {
      active:0,
      tab2active:0,
      isscroll:false,
      dataobject:{},
      dataList:[],
      skillsid:''
    };
  },
  created() {
    // this.skillsid =this.$route.query.skillsid;
    this.skillsid="2"
    var params ={ cmd: "skillsdetail",skillsid:this.skillsid};
    this.postRequest(params).then(res => {  
          console.log(res)
          this.dataobject = res.data.dataobject
    });

    var params2={ cmd: "skillsfirstmessagelist",skillsid:this.skillsid,nowPage:'1',pageCount:'10'}
    this.postRequest(params2).then(res => {       
          console.log(res.data.dataList)
          this.dataList = res.data.dataList
    });
  },
  mounted() {
    window.addEventListener('scroll',this.scrollLoad,true)
  },
  methods: {
    tab2cg(num){
      this.tab2active = num
    },
    // scrollLoad(){
    //   this.$nextTick(() => {
    //       var scrollTop =document.body.scrollTop || document.documentElement.scrollTop;          
    //       if(scrollTop>0){
    //         this.isscroll = true
    //       }else{
    //         this.isscroll = false
    //       }
    //   })
    },
  // }
    
};
</script>

<style scoped>
.bold{font-weight: bold;}
.pw{height: 50px;line-height: 50px;border-bottom: 1px solid #EEEEEE;}
.replay{height: 50px;width:300px;background: #F3F3F3;border-radius:10px; margin: 5px 0;padding: 5px 10px 2px;}
.replay p{height: 22px;line-height: 22px;}
.respan{color: #333;font-weight: bold;}
.c666{color: #666;}
.more{color: #2076FF;}

.btmbar{position: fixed;bottom: 0;height: 50px;left: 0;width: 100%;line-height: 50px;}
.btmbar ul{display: flex;flex-flow: row;width: 100%;height: 100%;}
.btmbar ul li{width: 33.33%;height: 100%;text-align: center;font-size: 15px;}
.bg0{color: #333;background: #fff;}
.bg1{color: #fff;background: #FF7519;}
.bg2{color: #fff;background: #2076FF;}

.starpricre{width: 40% !important;}
.icon{width: 14px;height:14px ;}
.c333{color: #333;font-size: 15px;font-weight: 600;}
.detail>img{width:100px;height: 100px; display: block;margin: 8px 0;}
.detail p{vertical-align:middle;}
.c9{color: #999;font-size: 12px;font-weight: normal;}
.p2{width: 100%;display: flex;flex-flow: row;justify-content: space-between;height: 30px;line-height: 30px;font-size: 15px;font-weight: bold;}
.ul1{display: flex;flex-flow: row;border-bottom: 1px solid #EEEEEE;padding: 5px 0 15px;}
.ul1 li{color: #666666;font-size: 14px;}
.first{text-align: left;border-right: 1px solid #EEEEEE;margin-right: 15px;padding-right: 15px;}
.p1{font-size: 15px;font-weight: bold;height: 40px;line-height: 40px;}
.p3{line-height: 22px;color: #333;font-size: 13px;}
.p1 .corg{margin-right: 10px;}
.corg{color: #FF7519!important;}
.bg{position:absolute;top: 0;left: 0;width: 100%;height: 200px;}
.box {
  width: 100%;
  box-sizing: border-box;
  background: #fff;
  padding-bottom: 50px;
}
.line{height: 8px;width: 100%;background:#FAFAFA; }
.top{
  width: 90%;
  height: 150px;
  background: #fff;
  border-radius: 6px;
  margin: 85px auto 0;
  position: relative;
  border: 1px solid #fff;
  box-shadow:0 0px 6px rgba(100, 100, 100, 0.4);
  margin-bottom: 12px;

}
.lyavator{border-radius: 50%;height:34px;width:34px;margin-right: 5px;}
.avtor{border-radius: 50%;position: absolute;left: 50%;top: 0;transform: translate(-50%,-50%);width: 70px;}
.s1{position: absolute;right: 6px;top:6px;display: block;width: 60px;height: 22px;border-radius: 5px;color: #fff;background: #2076FF;text-align: center;line-height: 22px;font-size: 13px;}
.pcom{height: 40px;width: 100%;line-height:40px;margin-top: 35px; text-align: center;color: #333;font-size:16px; border-bottom: 1px solid #EEEEEE;font-weight: 600;}
.ut{height: 75px;width: 100%;display: flex;flex-flow: row;align-items: center;}
.ut li{width: 25%;text-align: center;height: 45px;line-height: 45px;font-size: 13px;}
.ut li+li{border-left: 1px solid #EEEEEE;}
.con,.con2{
  padding: 0 12px 10px;
}
.liuptitle{
  height: 40px;
  line-height: 40px;
  font-size: 15px;
}
.liuptitle span{
  display: inline-block;
  margin-right: 10px;
  height: 100%;
}
.actived{
  color: #2076FF;
  border-bottom: 2px solid #2076ff;
}
.liuycontent li{
  display: flex;
  flex-flow: column;
  padding: 10px 3px;
  border-bottom: 1px solid #EEEEEE;
}
.topflex{
  display: flex;
  flex-flow: row;
  align-items: center;
  justify-content: space-between;
}
.middle,.bottom,.replay{
  width: calc(100% - 44px);
  margin-left: 44px;

}
.middle{
  line-height: 18px;
}
.bottom{
  display: flex;
  flex-flow: row;
  margin-top: 10px;
  justify-content: space-between;
}
.time{
  color: #999;
}
.option span{vertical-align:middle;margin:0 5px;}
</style>
