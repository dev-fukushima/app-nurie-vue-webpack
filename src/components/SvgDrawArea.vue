<template>
<div class="drawArea">
    <div class="fukidashi step4">
      <img src="img/think_fukidashi.png" alt="画像を長押しして保存してください">
    </div>
  <div id='dom' class="domArea col-12 step2" ref="dom"></div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  props:['svgsrc','setcolor'],
  data(){
    return{
      response:'',
      selected_path_object:null
    }
  },
  watch:{
    svgsrc:{
      immediate: true,
      deep: true,
      handler(val,changed){
        let _this = this;
        if(val){
        axios(val).then(function(response){
         _this.response = response;
         _this.$refs.dom.innerHTML = '';
         _this.$refs.dom.insertAdjacentHTML('beforeend',_this.response.data);
         _this.resizeSvg();
         _this.setPathClickEvent();
        });
        }
      }
    },
    setcolor:{
      immediate: true,
      deep: true,
      handler(val,changed){
        let color = val,
        _this = this;

        if(!color) return;

        if(_this.selected_path_object) _this.selected_path_object.setAttribute('fill',color);
        //if(pathobj) pathobj.css('opacity', 1);
        return false;
      }
    }
  },
  methods:{
    resizeSvg(){
      let _width = window.outerWidth,
      _svg = this.$refs.dom.getElementsByTagName('svg')[0];
      this.$refs.dom.style.minHeight = _width;
      _svg.style.width = _width;
      _svg.style.height = _width;

    },
    setPathClickEvent(){
      let _pathObj = document.querySelectorAll('path,circle,polygon'),
      _this = this,
      pathClickEvent = function(e){
        _this.selected_path_object = e.currentTarget;
        _pathObj.forEach(function(t){
          t.removeAttribute('class');
        })
        _this.selected_path_object.classList.add('selectedpath');

      };
      _pathObj.forEach(function(t){
        t.removeEventListener('click',pathClickEvent);
        t.addEventListener('click',pathClickEvent,false);
      })
    }
  }
}
</script>

<style lang="scss">

#dom {
display: block;
position: static;
left: 0px;
top: 0px;
width: 100%;
.makeimg {
  opacity: 0;
  transform-origin: center center;
  transition: all .4s linear;
}
svg{
  width: 100%;
  height: auto;
}
img{
  width: 100%!important;
  height: auto!important;
}
.selectedpath {
  transition: all .4s linear;
  stroke:#CE547F;
  stroke-width:8px;
 }
}
</style>
