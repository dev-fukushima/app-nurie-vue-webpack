
<template>
  <div class="app is-step1">
  <header class="headerArea">
      <h1>
        <img src="img/thankyou_img01.png" alt="">
      </h1>
      <div class="txArea Area-01 fireworks">

      <p>好きな色でキャラクターを塗って画像を保存しましょう。</p>
      </div>
    </header>
    <p class="nuriettl">
      <img src="img/thankyou_img03.png" alt="" id="mask">
    </p>
    <div class="txArea Area-02">
      <div class="exTextArea">
      <p class="tx-01">スマホで遊べるぬりえです。好きな色にぬってオリジナルの動物を作ることができます。作ったぬりえはLINEやFacebookのアイコンにもすることができます。</p>
      </div>
      <p class="tx-02 step1 step2">
        <img src="img/thankyou_img04_ttl.png" alt="1,ぬるキャラを選ぶ">
      </p>
    </div>
    <Items @stepUpdate="stepUpdate"></Items>
    <SvgDrawArea ref="svgDrawArea" :setcolor="selectedcolor" :svgsrc="loadedsvg"></SvgDrawArea>
    <Colors @selectedColor="selectedColor"></Colors>
    <div id="makebox" class="step2" @click="makeImg">
      <span id="make" class="btn">
        <img src="img/thankyou_saveBtn.png" alt="決定する">
      </span>
    </div>
    <footer>
      <span>Copyright &copy; example.com All Rights Reserved.</span>
    </footer>
  </div>
</template>

<script>
import Items from './Items'
import Colors from './Colors'
import SvgDrawArea from './SvgDrawArea'

export default {
    data(){
      return {
        loadedsvg :'',
        selectedcolor:'',
        selectedSvgData:null
      }
    },
    components: {
        Colors,
        Items,
        SvgDrawArea
    },
    methods:{
      stepUpdate(step,_path){
        let _app = document.querySelectorAll('div.app');
        _app[0].classList.remove('is-step1','is-step2','is-step3','is-step4');
        _app[0].classList.add(step);
        if(_path){
          this.loadedsvg = _path;
        }
      },
      imageToBase64(img, mime_type) {
          let canvas = document.createElement('canvas'),
          ctx = canvas.getContext('2d');
          canvas.width  = img.width;
          canvas.height = img.height;
          ctx.drawImage(img, 0, 0,img.width,img.height);
          // To Base64
          return canvas.toDataURL(mime_type);
      },
      selectedColor(_color){
        this.selectedcolor = _color;
      },
      makeImg(){

      let _this = this,
      svg = document.getElementsByTagName('svg')[0],
      data = new XMLSerializer().serializeToString(svg),
      url = "data:image/svg+xml;charset=utf-8;base64," + btoa(unescape(encodeURIComponent(data))),
      //img = $('<img>',{'class':'dlsvg',width:WIDTH,height:HEIGHT});
      img = new Image();
      img.className = 'dlsvg';
      img.width = 640;
      img.height = 640;

      let background = document.querySelectorAll('rect')[0].getAttribute('fill');

      img.onload = function(e){
        let src = _this.imageToBase64(e.currentTarget,'image/png'),
        _drawimg = new Image();
        _drawimg.width = e.currentTarget.width;
        _drawimg.height = e.currentTarget.height;
        _drawimg.className = 'makeimg';
        _drawimg.onload = function(e){
            let _dom = _this.$refs.svgDrawArea.$refs.dom;
            _dom.innerHTML = '';
            _dom.appendChild(e.currentTarget);
            _this.stepUpdate('is-step3');
            _this.$refs.svgDrawArea.$refs.dom.getElementsByTagName('img')[0].style.opacity = 1;
            setTimeout(function(){
              document.querySelectorAll('img.makeimg')[0].classList.add('bounceIn','animated');
            },400);
            setTimeout(function(){
              let _fuki = document.querySelectorAll('div.fukidashi')[0];
              _fuki.style.display = 'block';
              _fuki.classList.add('bounceIn','animated');
            },800);
        }
        _drawimg.src = src;

      }
      /*
      img.on('load',function(){
        var src = ImageToBase64($(this).get(0),'image/png');
        //var src = $(this).attr('src');
        var Render = {
          'response':function(res){
            //var $img = $('<img>',{'src':res.data,width:WIDTH,height:HEIGHT,'class':'makeimg','crossOrigin':'Anonymous'});
            var $img = $('<img>',{'src':res.data,width:WIDTH,height:HEIGHT,'class':'makeimg'});

            $('#dom').html($img);
            if(navigator.userAgent.indexOf('Android 4.0') > -1 || navigator.userAgent.indexOf('Android 4.1') > -1 || navigator.userAgent.indexOf('Android 4.2') > -1 || navigator.userAgent.indexOf('Android 4.3') > -1){
                var a = $('<a>',{'class':'attention','href':res.data,'text':'※保存できない場合はこちらをクリックして、リンク先画像を保存してください'});
                $('#dom').append(a);
            }
            $('#dom').css('opacity',1);
            setTimeout(function(){$('.makeimg').addClass('bounceIn animated');},400);
            setTimeout(function(){$('.fukidashi').show().addClass('bounceIn animated');},800);
            make.remove();
            itembox.remove();
            colorbox.remove();
            step1.hide();
            step2.hide();
            step3.show();
            $(window).off().on('resize orientationchange',function(){
              DrawTool.resetItemsize();
            });

          }},
          request = {
          'url':document.URL,
          'type':'POST',
          'data':{
            image:src,
            width:WIDTH,
            height:HEIGHT,
            id:id,
            background:background
          },
          'dataType':'json',
          'success':function(res){
            Render.response(res);
          },
          'error':function(jqXHR,textStatus,errorThrown){
                 console.log('------render error----');
                 console.log(jqXHR, textStatus, errorThrown);
                 make.remove();
            }
        }

        $.ajax(request);
      });
      */
      //img.get(0).setAttribute('crossOrigin','Anonymous')
      img.setAttribute('src', url);
      return false;
      }
    }
}
</script>

<style lang="scss">
.text-red{
  color:#cff;
}
footer{
display:flex;
justify-content:center;
align-items:center;
padding:10px 0;
color:#fff;
font-size:10px;
background:#000;
width:100%;
}
</style>
