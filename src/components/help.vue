<template>
    <div style="height:100vh"> 
         <p class="liuptitle">
             详情
        </p>
        <!-- <div class="line"></div> -->
        <div class="con2">
            <section class="liuycontent">
                <ul>        
                   <li v-for="(item,index) in dataList" :key="index">
                    <div class="topflex">
                        <img :src="item.usericon" alt="" class="lyavator">
                        <div style="width:100%;">
                            <div class="ddd">
                                <span class="c333">{{item.username}}</span>
                                <span class="c9">浏览量：2551</span>
                            </div>                            
                            <div class="time">
                                发布时间：{{item.time}}
                            </div>
                        </div>
                        
                    </div>
                    <div class="middle">
                  {{item.content}}
                    </div>
                   <div class="detail">
                        <img :src="i" alt="" v-for="i in item.images" :key="i">
                         <p>
                            <img src="@/assets/images/di.png" alt="" style="width:9px;height:11px;">
                            <span style="color:#A5A5A5;">商都世贸中心D座</span>
                        </p>  
                    </div>
                </li>
                
                </ul>
            </section>
            </div>
    </div>
</template>
<script>
export default {
  data() {
    return {
      dataList:[],
      uid:'',
      city:''
    };
  },
  created() {
    this.city =this.$route.query.city
    var params ={ cmd: "welfareslibrary", city:this.city,nowPage:'1',pageCount:'10'}
    this.postRequest(params).then(res => {       
          console.log(res)
          this.dataList = res.data.dataList
    });
  },
}
</script>
<style scoped>
.detail{padding: 5px 10px;}
.detail>img{width:100px;height: 100px; display:inline-block;margin: 4px;}
.ddd{    
  display: flex;
  flex-flow: row;
  justify-content: space-between;
}
.c333{font-size: 15px;font-weight: bold;}
.line{height: 8px;width: 100%;background:#FAFAFA; }
.con2{
  padding: 0 12px 10px;
  width: 100vw;
  border-radius: 10px;
  background: #fafafa;
}
.c9{color: #999;font-size: 13px;font-weight: normal;}
.liuptitle{
  height: 50px;
  line-height: 50px;
  font-size: 16px;
  font-weight: bold;
  background: #fff;
  text-align: center;
}
.liuptitle span{
  display: inline-block;
  margin-right: 10px;
  height: 100%;
}
.liuycontent li{
  display: flex;
  flex-flow: column;
  padding: 10px 3px;
  background: #fff;
  border-radius: 5px;
  margin-top: 10px;
}
.topflex{
  display: flex;
  flex-flow: row;
  align-items: center;
}
.middle,.bottom,.replay{
  width: 100%;

}
.middle{
  line-height: 18px;
  font-size: 13px;
  margin: 10px 0; 
  padding: 0 10px;
}
.bottom{
  display: flex;
  flex-flow: row;
  margin-top: 10px;
  justify-content: space-between;
}
.time{
  color: #999;font-size: 14px;margin-top: 10px;
}
.option span{vertical-align:middle;margin:0 5px;}
.icon{width: 14px;height:14px ;}
.lyavator{border-radius: 50%;height:49px;width:49px;margin-right: 5px;}
</style>
