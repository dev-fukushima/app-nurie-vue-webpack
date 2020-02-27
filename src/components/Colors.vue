<template>
<div class="step2">
  <div class="step2_text">
    <img src="img/thankyou_img05.png" alt="2,エリアをタップして塗る">
  </div>
<div class="colorboxWrap">
    <div class="colorbox" id="colorbox">
      <div id="colorBtnArea">
        <ul class="cf">
          <li v-for="color in colors">
            <span @click="selectColor" :data-color="color.color" :style="{background:color.color}"></span>
          </li>
        </ul>
      </div>
    </div>
    <!--
    <ul class="arr">
      <li class="left-arr"><img src="img/arr_left.png" alt=""></li>
      <li class="right-arr"><img src="img/arr_right.png" alt=""></li>
    </ul>
    -->
</div>
</div>
</template>

<script>
export default{
  data:function(){
  return {
    colors:[
        {'color':'#a7dbd1'},
        {'color':'#c4e6be'},
        {'color':'#b5cfe0'},
        {'color':'#cebed4'},
        {'color':'#d9d0c9'},
        {'color':'#efd25c'},
        {'color':'#62afa0'},
        {'color':'#50946c'},
        {'color':'#3d6c8b'},
        {'color':'#906d9f'},
        {'color':'#5f4f43'},
        {'color':'#e59b27'},
        {'color':'#42746a'},
        {'color':'#225c3a'},
        {'color':'#1c4057'},
        {'color':'#553562'},
        {'color':'#412e1f'},
        {'color':'#7d5d2b'},
        {'color':'#e0b173'},
        {'color':'#eaa1ba'},
        {'color':'#ec9f97'},
        {'color':'#FFFFFF'},
        {'color':''},
        {'color':''},
        {'color':'#d68148'},
        {'color':'#ce547f'},
        {'color':'#c1554a'},
        {'color':'#d4d5d5'},
        {'color':''},
        {'color':''},
        {'color':'#a6541e'},
        {'color':'#923455'},
        {'color':'#923c33'},
        {'color':'#4d5556'},
        {'color':''},
        {'color':''}
        ]
    }
  },
  methods:{
    selectColor(e){
      let _target = e.currentTarget,
      _selectColor = _target.getAttribute('data-color');
      this.$emit('selectedColor',_selectColor);
    }
  }
}

</script>

<style lang="scss" scoped>

#colorbox {
  overflow-x:scroll;
  &.active {
    display: block;
  }
  ul {
    padding: 5px 0;
  }
  .owl-item {
    width: 100%!important;
    float: left;
  }
  .owl-stage {
    width: 100%!important;
  }
}


#colorBtnArea {
    li {float:left; margin-right:1%;margin-bottom:1rem;width: 15%;
      &:nth-child(6n){
        margin-right: 0;
        }
    }
    li span{
      border-radius: 50%;
      width: 40px;
      height: 40px;
      display: block;
      cursor:pointer;
      margin: 0 auto;
    &[data-color="#FFFFFF"]{
      border: 1px solid #ccc;
    }
    &:after{
      display: block;
      content:" ";
      width: 50px;
      height: 50px;
      position: relative;
      left:-5px;
      top: -5px;
      border:none;
      border-radius: 50%;
    }
    &.selected:after{
      display: block;
      content:" ";
      width: 50px;
      height: 50px;
      position: relative;
      border-radius: 50%;
      border:4px solid #1F874A;
      left:-5px;
      top: -5px;
      transition: all .4s linear;
    }
    }
    ul{
      position: relative;
      float: left;
    }
}

</style>
