<template>
    <div class="carousel">
      <div class="carousel-con" id="carouselContent">
        <slot>没有内容</slot>
      </div>
      <div class="carousel-index">
        <ul id="con-index">
          <li v-for="row in contentNum"  @click="changeContent(row)"></li>
        </ul>
      </div>
      <div class="carousel-lefticon" @click="changeContent('PRE')">
        <img src="../../static/images/carouselLeft.png" class="lefticon"/>
      </div>
      <div class="carousel-righticon" @click="changeContent('NEXT')">
        <img src="../../static/images/carouselLeft.png" class="righticon"/>
      </div>
    </div>
</template>

<script>
export default {
  name:"carousel",
  data(){
    return {
      //carouselList:["carousel"],
      activeIndex: 0,
      contentNum: 1
    }
  },
  created () {

  },
  mounted:function(){
    this.changeContent()
    this.contentNum = this.getContentNum()
    this.autoPlay()
  },
  methods:{
    changeContent(val){
      var nowIndex=this.activeIndex;//原来的active轮播页数
      if(val=="NEXT"){
        if(this.activeIndex+1<this.contentNum ){
          this.activeIndex++
        }else if(this.activeIndex+1>=this.contentNum){
          this.activeIndex=0
        }
      }else if(val=="PRE"){
        if(this.activeIndex-1>=0 ){
          this.activeIndex--
        }else if(this.activeIndex-1<0){
          this.activeIndex=this.contentNum-1
        }
      }else if( (/^\d*$/).test(parseInt(val))){
        this.activeIndex=parseInt(val)-1;
        // document.getElementById("con-index").children[val-1].add("active-li")
      }
      // else if(isNumber(parseInt(val))){
      //   this.activeIndex=val;
      // }
      this.changeActiveContent(nowIndex)
    },
    changeActiveContent(preIndex){
      var el = document.getElementById("carouselContent");
      //      this.contentNum=el.childElementCount
      el.children[preIndex].classList.remove("carousel-item-active")
      el.children[preIndex].classList.add("carousel-item")
      el.children[this.activeIndex].classList.remove("carousel-item")
      el.children[this.activeIndex].classList.add("carousel-item-active")
      document.getElementById("con-index").children[preIndex].classList.remove("active-li")
      document.getElementById("con-index").children[this.activeIndex].classList.add("active-li")
    },
    getContentNum(){
      if(document.getElementById("carouselContent")!= null || document.getElementById("carouselContent")!= undefined){
        return document.getElementById("carouselContent").childElementCount
      }else{
        return 1;
      }
    },
    autoPlay(){

      setInterval(() => {

        var nowIndex = this.activeIndex;//原来的active轮播页数
        if(this.activeIndex + 1 < this.contentNum ){
          this.activeIndex++
        }else if(this.activeIndex+1>=this.contentNum){
          this.activeIndex=0
        }
        this.changeActiveContent(nowIndex)
//        console.log("每秒钟输出nowIndex"+nowIndex+"activeIndex"+this.activeIndex)
      }, 5000)
    }
  },
  watch: {

  },
  computed: {
    // contentNum: function () {
    //   if (document.getElementById("carouselContent").childElementCount){
    //     return document.getElementById("carouselContent").childElementCount
    //   } else {
    //     return 0;
    //   }
    // }
  }
}
</script>

<style scropd >
.carousel{
  position: relative;
  width: 80%;
  height: 370px;
  text-align: center;
  background-color: #bdbdbd;
  /*margin-top: 60px;*/
}
  .carousel-index{
    margin-left: -50px;
    /*width: 100px;*/
    padding: 2px 20px;
    height: 20px;
    position: absolute;
    bottom: 10px;
    left: 50%;
    border-radius: 50px;
    background-color: rgba(151, 151, 151,0.6);
  }
.carousel-con{
  height: 100%;
  width: 100%;
  white-space:nowrap;
}
  .carousel-lefticon{
    position: absolute;
    top: 50%;
    left:10px;
    margin-top: -25px;

  }
.carousel-righticon{
  position: absolute;
  top: 50%;
  right: 10px;
  margin-top: -25px;
}
.lefticon,.righticon{
  width: 50px;
  height: 50px;
  opacity:0.5;

}
  .righticon{
    transform:rotate(180deg) ;
  }

/*.carousel-con1{*/

  /*background-color: orange;*/
/*}*/

.carousel-item-active{
  height:100%;
  width: 100%;
  /*background-color: orange;*/
  display: block;
}
  .carousel-item{
    height:100%;
    width: 100%;
    display: none;

  }

  .carousel-index ul{
    /*background-color: #42b983;*/
    /*position: absolute;*/
    list-style: none;
    margin: 0;
    padding: 0;
    /*left: 0;*/
  }
li{
  border-radius: 5px;
  width: 10px;
  height:10px;
  display: inline-block;
  margin:0 5px !important;
  display: inline-block;
  background-color: rgba(255,255,255,0.5);
}

.active-li{
  background-color: rgba(255,255,255,1);
}

.carousel-img{
  max-height: 100%;
  /*max-width: 100%;*/
  width: 100%;
  /*height: 100%;*/
}

</style>
