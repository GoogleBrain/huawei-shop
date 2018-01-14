<template>
  <div class="information">
        <div class="informationHeader">
            <img src="http://clubstyle.dbankcdn.com/template/hw_fans/image/zh/css/img/huaweilogo.png" alt="">&nbsp;&nbsp;<span>花粉俱乐部</span>&nbsp;&nbsp;<img src="http://clubstyle.dbankcdn.com/template/hw_fans/image/zh/css/img/forlove.png" alt="">
        </div>
        <div class="swipe2">
            <mt-swipe :auto="4000">
                <mt-swipe-item><img src="http://clubimg.dbankcdn.com/data/attachment/portal/201801/04/194823jrjtgjhdagldk68p.jpg" alt="轮播图"></mt-swipe-item>
                <mt-swipe-item><img src="http://clubimg.dbankcdn.com/data/attachment/portal/201801/05/155115nbfu6e94vr9hwhho.jpg" alt="轮播图"></mt-swipe-item>
                <mt-swipe-item><img src="http://clubimg.dbankcdn.com/data/attachment/portal/201801/04/194833pfiuwstbm8phbty5.jpg" alt="轮播图"></mt-swipe-item>
                <mt-swipe-item><img src="http://clubimg.dbankcdn.com/data/attachment/portal/201801/05/234644ath5qq8dwhikydju.jpg" alt="轮播图"></mt-swipe-item>
            </mt-swipe>
        </div>
        <div class="informationMian">
            <ul>
                <li v-for="(information,index) in informations" class="Mainlist" @click="open(information.id)" :id="information.id">
                    <h3 class="MainTitle" style="color:#434343"> {{information.title}}</h3  >
                    <span class="MianTime">{{information.time}}</span>
                    <div class="informationImg">
                        <img  v-bind:src="information.img" alt="图片">
                    </div>
                    <a href="">阅读全文</a>
                </li>
            </ul>
            
        </div>
        <div class="informationfooter">

        </div>
  </div>
</template>

<script>
import { Swipe, SwipeItem } from 'mint-ui';
export default {
    name:"information",
    data(){
        return{
            informations:[]
        }
    },
    mounted:function(){
        this.getDate()
    },
    methods:{
        getDate:function(){
            var _this=this;
            this.$http.get("/static/information.json").then(function(res) {
                for (var i = 0, len = res.body.informations.length; i < len; i++) {
                    var selData = res.body.informations[i];
                    var part = res.body.informations[i].name;
                    _this.informations.push(selData);
                }
            })
        },
        open:function(id){
            this.$router.push({path:"news",query:{id:id}})
        },
    }

  
}
</script>


<style>
.informationHeader{
    position: fixed;
    width: 100%;
    -webkit-box-shadow: 0 0 10px #cecece;
    box-shadow: 0 0 10px #cecece;
    height: 1.3rem;
    line-height: 1.3rem;
    font-size: 0.35rem;
    padding-left: 0.3rem;
    background: white;
    top: 0;
    font-size: 0.41rem; 
}
.informationHeader i{
    display: block;
    float: left;
    height: 50px;
    padding-left: 0.3rem;
    font-size: 22px;
    color: black;
}
.informationHeader img{
    position: relative;
    top:0.1rem;
}
 .swipe2{
     height: 6.5rem;
     margin-top: 70px;
   }
   .swipe2 img{
      width: 100%;
      height: 6.5rem;
  }
.Mainlist{
    width: 100%;
    height: 7rem;
    background: white;
    margin-top: 5px;
    padding-top: 0.35rem;
}

.MainTitle{
    width: 77%;
    text-align: left;
    margin: auto;
    color: rgb(67, 67, 67);
    font-size: 0.4rem
}
.MianTime{
    width: 78%;
    margin: auto;
    display: block;
    line-height: rem;
    padding: 7px 36px;
    font-size: 0.1rem;
}
.informationImg img{
    width: 100%;
    height: 4.7rem;
}
.Mainlist a{
    float: right;
    font-size: 0.3rem;
    margin-right: 0.75rem;
    margin-top: 0.2rem;
    color: black;
}
</style>
