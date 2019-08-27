<template>
  <div>
  
         <p class="liuptitle2">帖子详情</p>
  
   
    <div class="box2 pd">
      <ul class="ubox">
        <li>
          <span class="s1">关注</span>
          <img :src="dataobject.usericon" class="avtor4" alt />
          <span class="bspan">
            <span class="p14">{{dataobject.username}}</span>
            <span class="tim">发布时间：{{dataobject.time}}</span>
          </span>
          <p class="cblue pttit">{{dataobject.title}}</p>
          <p class="pcon">{{dataobject.content}}</p>
          <div>
            <!-- <img :src="dataobject.image" alt="" class="ci" v-for="i in dataobject.image" :key="i"> -->
            <img src="../../static/img/8.jpg" alt class="ci" />
            <img src="../../static/img/8.jpg" alt class="ci" />
            <img src="../../static/img/8.jpg" alt class="ci" />
            <img src="../../static/img/8.jpg" alt class="ci" />
            <img src="../../static/img/8.jpg" alt class="ci" />
          </div>
        </li>
      </ul>
    </div>
    <div class="line"></div>
    <div class="flex pd b3">
      <img :src="dataobject.circlesimage" class="avtor4" alt />
      <!-- <span class="s2">进入圈子</span> -->
      <div>
        <p class="p14">{{dataobject.circlestitle}}</p>
        <p class="c99">成员：{{dataobject.membercount}} . {{dataobject.dongtaicount}}条帖子</p>
      </div>
    </div>
    <div class="line"></div>
    <div class="con2">
      <p class="liuptitle">
        <span class="actived">留言 (3)</span>
        <!-- <span :class="tab2active==1?'actived':''" @click="tab2cg(1)">中标公示</span> -->
      </p>
      <section class="liuycontent">
        <ul>
          <li v-for="(item,index) in dataList" :key="index">
            <div class="topflex">
              <div>
                <img :src="item.usericon" alt class="lyavator" />
                <span class="c333">{{item.username}}</span>
              </div>
              <span class="c9">{{index+1}}楼</span>
            </div>
            <div class="middle">{{item.content}}</div>
            <div class="bottom">
              <div class="time">{{item.time}}</div>
              <div class="option">
                <img src="@/assets/images/news.png" alt class="icon" />
                <span>回复</span>
                <img src="@/assets/images/zan.png" alt class="icon" v-if="item.iszan==0" />
                <img src="@/assets/images/zan2.png" alt class="icon" v-if="item.iszan==1" />
                <span>{{item.zancount}}</span>
              </div>
            </div>
            <div class="replay" v-if="item.secondcount!=0">
              <p>
                <span class="respan">@{{item.username}}：</span>
                <span class="c666">先报名！</span>
              </p>
              <p class="more">共{{item.secondcount}}条回复></p>
            </div>
          </li>
        </ul>
      </section>
    </div>
    <footer>
      <input type="text" class="usepoint" v-model="pointmsg" placeholder="发觉不错说两句~" />
      <span class="sendmsg">发送</span>
      <div class="goodcont">
        <div class="goodzan">
          <img src="./../assets/images/zan.png" alt v-if="good" />
          <img src="./../assets/images/zan2.png" alt v-else />
        </div>
        <span class="goodnum">0</span>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      dataobject: {},
      dataList: [],
      did: "",
      good: true,
      pointmsg: ""
    };
  },
  created() {
    // this.did = this.$route.query.did
    this.did = "1";
    var params = {
      cmd: "circlesdynamicdetail",
      did: this.did
    };
    this.postRequest(params).then(res => {
      console.log(res);
      this.dataobject = res.data.dataobject;
    });
    var params2 = {
      cmd: "dynamiccommentlist",
      did: this.did,
      nowPage: "1",
      pageCount: "10"
    };
    this.postRequest(params2).then(res => {
      console.log(res);
      this.dataList = res.data.dataList;
    });
  },
  mounted() {},
  methods: {   
  }
};
</script>

<style scoped>
.back{
  position: absolute;
  top: 15px;
  left: 15px;
}
.liuptitle2 {
  height: 50px;
  line-height: 50px;
  font-size: 16px;
  font-weight: bold;
  background: #fff;
  text-align: center;
  border-bottom: 1px solid #f8f8f8;
}

.tim {
  color: #999;
  margin-top: 3px;
}

.bspan {
  display: inline-block;
  width: 90%;
  height: 40px;
  vertical-align: middle;
}

.bspan span {
  display: block;
  margin-top: 8px;
}

.replay {
  height: 50px;
  width: 300px;
  background: #f3f3f3;
  border-radius: 10px;
  margin: 5px 0;
  padding: 5px 10px 2px;
}

.replay p {
  height: 22px;
  line-height: 22px;
}

.respan {
  color: #333;
  font-weight: bold;
}

.c666 {
  color: #666;
}

.more {
  color: #2076ff;
}

.con,
.con2 {
  padding: 0 12px 10px;
  background: #fff;
}

.liuptitle {
  height: 40px;
  line-height: 40px;
  font-size: 15px;
}

.liuptitle span {
  display: inline-block;
  margin-right: 10px;
  height: 100%;
}

.actived {
  color: #2076ff;
  border-bottom: 2px solid #2076ff;
}

.liuycontent li {
  display: flex;
  flex-flow: column;
  padding: 10px 3px;
  border-bottom: 1px solid #eeeeee;
}

.topflex {
  display: flex;
  flex-flow: row;
  align-items: center;
  justify-content: space-between;
}

.middle,
.bottom,
.replay {
  width: calc(100% - 44px);
  margin-left: 44px;
}

.middle {
  line-height: 18px;
}

.bottom {
  display: flex;
  flex-flow: row;
  margin-top: 10px;
  justify-content: space-between;
}

.lyavator {
  border-radius: 50%;
  height: 34px;
  width: 34px;
  margin-right: 5px;
}

.time {
  color: #999;
}

.option span {
  vertical-align: middle;
  margin: 0 5px;
}

.c99 {
  color: #999;
  /* margin-left: 5px; */
  margin-top: 10px;
}

.b3 {
  background: #fff;
  position: relative;
}

.btp {
  color: #999;
  font-size: 14px;
  text-align: center;
  height: 50px;
  line-height: 50px;
}

.option span {
  vertical-align: middle;
  margin: 0 25px 0 5px;
}

.option {
  height: 40px;
  line-height: 40px;
}

.icon {
  width: 14px;
  height: 14px;
}

.cblue {
  color: #2076ff;
}

.pttit {
  height: 50px;
  line-height: 60px;
  font-size: 13px;
}

.pcon {
  line-height: 18px;
}

.p14 {
  font-size: 15px;
  /* margin-left: 5px; */
}

.ubox li {
  border-radius: 6px;
  padding-bottom: 10px;
  position: relative;

  padding-top: 10px;
}

.ci {
  height: 83px;
  width: 100px;
  margin: 5px 10px 4px 0;
  border-radius: 3px;
}

.s13 {
  font-size: 13px;
  color: #222;
}

.lou {
  display: flex;
  flex-flow: row;
  align-items: center;
  justify-content: space-between;
  padding: 18px 0;
}

.arrow {
  width: 8px;
  height: 16px;
}

.box2 {
  position: relative;
  width: 99.88%;
  background: #fff;
  z-index: 3;
  padding-bottom: 20px;
}

.pd {
  padding: 0 15px;
}

.p16 {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 6px;
}

.p12 {
  font-size: 12px;
}

.flex {
  display: flex;
  flex-flow: row;
  align-items: center;
  padding: 12px;
}

.line {
  height: 6px;
  width: 100%;
  background: #fafafa;
}

.topbox {
  position: relative;
  color: #fff;
  z-index: 2;
}

.avtor {
  border-radius: 10px;
  width: 60px;
  border: 2px solid #ddd;
}

.avtor3 {
  width: 34px;
  border-radius: 50%;
  border: 2px solid #fff;
}

.avtor4 {
  width: 44px;
  border-radius: 12px;
}

.s1 {
  position: absolute;
  right: 10px;
  top: 12px;
  display: block;
  width: 60px;
  height: 22px;
  border-radius: 5px;
  color: #fff;
  background: #2076ff;
  text-align: center;
  line-height: 22px;
  font-size: 14px;
}

.s2 {
  position: absolute;
  right: 10px;
  top: 20px;
  display: block;
  width: 81px;
  height: 26px;
  border-radius: 13px;
  color: #fff;
  background: #2076ff;
  text-align: center;
  line-height: 26px;
  font-size: 13px;
}
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 50px;
  z-index: 99;
  background: #fff;
  box-shadow: 0 0 2px #ddd;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 15px;
}
.usepoint {
  width: 235px;
  height: 28px;
  background: #ddd;
  border-radius: 15px;
  padding-left: 15px;
}

footer .sendmsg {
  color: #2076ff;
}
footer .goodzan {
  width: 15px;
  height: 15px;
  position: relative;
}
.goodcont {
  display: flex;
  align-items: center;
}
.goodzan img {
  position: absolute;
  top: 0;
  width: 100%;
  height: auto;
}
.goodnum {
  display: block;
  margin-left: 5px;
}
</style>
