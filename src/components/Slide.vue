<template>
  <div class="slide">
    <transition-group name="slide-fade" :duration="{ enter: 500, leave: 800 }" tag="ul">
      <li v-for="(item,index) in slideList" :key="index" v-show="index===showImg"><img :src="require(`@/assets/${item}.jpg`)"></li>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: 'Slide',
  props: {
    slideList: Array,
  },
  data: function () {
    return {
      showImg: 0
    }
  },
  mounted: function () {
    setInterval(this.slide, 10000);
  },
  methods:{
    slide(){
      if(this.showImg<this.slideList.length-1){
        this.showImg++
      }else{
        this.showImg = 0
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.slide {
  position: relative;
  height: 28vw;
  overflow: hidden;
  border-bottom: solid 5px #333;
  margin-bottom: 15px;
}
.slide li {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
}
.slide img {
  width: 100%;
}
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
