<template>
<div>
  <div class="box" ref="box">
    <div class="inner"
    v-for="(color,index) in data"
    :style="{backgroundColor:color,opacity:index==flag?1:0}"
    >
        {{index}}
    </div>
  </div>
  <div class="line">
    <div v-for="(ele,index) in data"
    :style="{backgroundColor:flag==index?'red':'yellow'}"
    v-on:mouseenter="clickLine(index)"
    v-on:mouseleave="moveByTime"
    ></div>
  </div>
   <button  @click="next">下一页</button>
</div>
</template>
<script>
export default {
  name: 'hello',
  data () {
    return {
        flag:0,
        data: ["red", "blue", "grey", "orange"],
        move:null
    }
  },
  methods:{
    next(){
    this.clearTime()
    this.moveByTime()
        if(this.$data.flag<this.$refs.box.children.length-1){
          this.$data.flag+=1
        }else{
         this.$data.flag=0
        }
    },
    moveByTime(){
      this.$data.move=setInterval(this.next,2000)
    },
    clearTime(){
      clearInterval(this.$data.move)
    },
    clickLine(index){
    this.clearTime()
      this.$data.flag=index
    }
  },
  mounted(){
    this.moveByTime()
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box{
    width:500px;
    height:300px;
}
.box>div{
    width:500px;
    height:300px;;
    position: absolute;
    opacity: 0;
    font-size: 50px;
    line-height:300px;
    transition: all 0.5s;
    background-color:red;
}
.line{
width:120px;
height:20px;
}
.line>div{
  width:20px;
  height:20px;
  margin:0 5px;
  background-color:blue;
  border-radius:50%;
  float:left;
}
</style>
