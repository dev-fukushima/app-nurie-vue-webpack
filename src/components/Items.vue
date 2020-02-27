<template>
<div class="step1 step2" id="itembox">
  <div id="itemArea" class="itemArea">
    <div v-for="item in items" class="itembtn"><span class="border"></span><span class="item" :data-svg="item.svgdata" @click="selectItem"><img :src="item.btnsrc"></span></div>
  </div>
  <ul class="arr">
    <li class="left-arr"><a href="#" class="btn-left"></a></li>
    <li class="right-arr"><a href="#" class="btn-right"></a></li>
  </ul>
</div>
</template>

<script>
export default{
  data:function(){
  return {
    items:[{"btnsrc":"img/btn01.png","svgdata":"svg/01.svg"},
      {"btnsrc":"img/btn02.png","svgdata":"svg/02.svg"},
      {"btnsrc":"img/btn03.png","svgdata":"svg/03.svg"},
      {"btnsrc":"img/btn04.png","svgdata":"svg/04.svg"},
      {"btnsrc":"img/btn05.png","svgdata":"svg/05.svg"},
      {"btnsrc":"img/btn06.png","svgdata":"svg/06.svg"}
      ]
    }
  },
  methods:{
    selectItem(e){
      let _target = e.currentTarget,
      _parent = _target.parentNode,
      _svgPath = _target.getAttribute('data-svg'),
      _btns = document.querySelectorAll('div.itembtn');
      _btns.forEach(function(t){
        t.classList.remove('selectedItem');
      });
      _parent.classList.add('selectedItem');
      this.$emit('stepUpdate','is-step2',_svgPath);

    }
  }
}

</script>

<style lang="scss" scoped>
#itemArea{
  width: 98%;
  padding: 0;
  margin: 2rem auto .5rem;
  min-height: 100px;
  ul{
   float: left;
   padding: 0;
   margin-bottom: 0;
  }
  .owl-item{
    float: left;
  }
  .itembtn{
  float: left;
  margin-right:1%;
  margin-bottom:1rem;
    width:24%;
    transition: all .4s ease;
    position: relative;
    box-sizing: border-box;
    .item {
      cursor: pointer;
      position: relative;
      .border{
        display: block;
        width: 100%;
        height: 100%;
        position: absolute;
        transition: all .4s ease;
      }
    }
    &.selectedItem .border{
      display: block;
      width: 100%;
      height: 100%;
      position: relative;
      z-index: 500;
      border: 4px solid #88c9be;
      position: absolute;
    }
    &:last-child{
      margin-right: 0;
    }
    img{width:100%;}
    }
}


</style>
