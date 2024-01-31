<script >
import ArrowLeft from '../assets/ArrowLeft.vue'

export default {
  components:{
    ArrowLeft
  },  
  data() {
      return {
        page: 1
      };
  },   
};
</script>

<template>
  <div class="container flex">
    <div class="card-intro">
        <div class="line-one top"></div>
        <div class="line-two top second"></div>
        <div class="line-one bottom"></div>
        <div class="line-two bottom second"></div>
      <div class="flex justify-center items-center w-full h-full overflow-hidden">
        <img                                        
            src="/image-intro.png"
            alt="Image intro"
            class="intro-img"
        />
      </div>
      <div class="title-intro">We Create</div>
      <div class="box-btn">      
        <div class="btn-intro" role="button">
          <div class="bg-btn" />
          <span>AWESOME THINGS</span>
          <ArrowLeft />
        </div>
      </div>
    </div>
  </div>  
</template>

<style lang="scss" scoped>
.container{
    min-height: 1024px;
    max-width: 100%;
    width: 100%;
    overflow: hidden;
    position: relative;
}
.card-intro{
  width: 961px;
  height: 598px;
  display: flex;
  position: relative;
  align-items: center;
  justify-content: center;
  margin: auto;
  .intro-img{
    width: auto;
    height: 100%;
    filter: grayscale(100%);
    transform: scale(1);
    transition: all 0.5s ease-in-out;
  }
  .title-intro {
    color: #FFB800;    
    font-size: 175px;
    font-weight: 700;
    position: absolute;
    top: -107px;
    left: -118px;
    transition: all 0.5s ease-in-out;
  }
  .box-btn{
    position: absolute;
    bottom: -78px;
    left: -126px;
    transition: opacity 0.6s ease-in-out;
    opacity: 0;    
    visibility: hidden;
  }
  .btn-intro{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 78px;
    position: relative;
    color: #FFB800;
    background: transparent;
    width: 1039px;
    height: 162px;
    border-radius: 15px;
    font-size: 72px;
    font-weight: 700;   
    transition: color 0.01s ease;
    &:hover{
      color: #FFFFFF;
      transition: color 0.1s ease-in-out;
      .bg-btn{
        left: 0;
      }  
    }
    .bg-btn{
      width: 100%;
      height: 100%;
      border-radius: 15px;
      background: #FFB800;
      position: absolute;
      transition: left 0.4s ease-in-out;
      left: -81vw;
      top: 0;
    } 
    span{
      transition: all 0.5s ease-in-out;
      transform: translateX(-61vw);
    }
    svg{
      width: 146px;
      height: auto;
      transition: all 0.5s ease-in-out;
      transform: translateX(33vw);
    }
  }
  
  .line-one, .line-two{
    position: fixed;
    height: 18px;
    background: #FFB800;
    width: 0;
    transition: all 0.4s ease-in-out;
    &.top{
      top: 50px;
      right: 210px;
      &.second{
        right: 50px;
      }
    }
    &.bottom{
      bottom: 50px;      
      left: 210px;
      &.second{
        left: 50px;  
      }
    }
  }
  
  &:hover{
    .intro-img{
      filter: grayscale(0);
      transform: scale(1.15);
    }
    .title-intro {    
      font-size: 185px;
    }
    .box-btn{      
      transition: opacity 0.4s ease-in-out;
      opacity: 1;
      visibility: visible;
    }
    .btn-intro{      
      span, svg{
        transform: translateX(0);
      }
    }
    .line-two{
        width: 140px;
      }
      .line-one{
        width: 67px;
      }
  }
}

</style>
