<script >
import ArrowLeft from '../assets/ArrowLeft.vue'
import ArrowBack from '../assets/ArrowBack.vue'

export default {
  components:{
    ArrowLeft,
    ArrowBack
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
    <div class="page-wrap" :class="{'to-left': page === 2}">
      <transition name="fade" mode="out-in">
        <div v-show="page === 1" class="card-intro">
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
          <div class="title-intro" :class="{out: page === 2}">We Create</div>
          <div class="box-btn" :class="{out: page === 2}">      
            <div class="btn-intro" role="button" @click="page = 2;">
              <div class="bg-btn" />
              <span>AWESOME THINGS</span>
              <ArrowLeft />
            </div>
          </div>
        </div>                
      </transition>
      <div class="card-menu" :class="{'show': page === 2}">
        <div class="wrap-menu">
          <div class="bg-menu-image">
            <div class="flex flex-col mx-auto img-wrap">
              <img src="/bg-menu-1.png" alt="About us"/>
              <img src="/bg-menu-2.png" alt="Our Product"/>
              <img src="/bg-menu-3.png" alt="Contact us"/>
            </div>
          </div>
          <ul>
            <li>About Us</li>
            <li>Our Product</li>
            <li>Contact Us</li>
          </ul>
        </div>
      </div>
      <div 
        class="btn-back" 
        v-if="page === 2" 
        @click="page = 1;" 
        role="button"
      >
        <ArrowBack/>
        <span>Back</span>
      </div>
    </div>
  </div>  
</template>

<style lang="scss" scoped>
.container{
    min-height: 1024px;
    max-width: 100%;
    height: 100vh;
    width: 100%;
    overflow: hidden;
    position: relative;
}
.page-wrap{  
  position: relative;
  width: 961px;
  height: 598px;
  margin: auto calc(50% - 480.5px) auto auto;
  transition: all 0.3s ease-in-out;  
  &.to-left{
    transition: all 0.3s ease-in-out 0.4s;
    margin: auto 0 auto auto;    
    width: 968px;
    height: 100vh;
  }  
}
.card-menu{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  visibility: hidden;
  opacity: 0;
  transition: opacity 0.4s ease-in-out, visibility 0.001s ease-in-out 0.3s;  
  &.show{
    transition: opacity 0.4s ease-in-out 0.4s, visibility 0.001s ease-in-out;    
    visibility: visible;
    opacity: 1;
  }
}
.wrap-menu{
  width: 100%;
  height: 100%;
  background: #2D2D2D;
  display: flex;
  position: relative;
  .bg-menu-image{
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    width: 100%;
    height: 100%;
    .img-wrap{
      width: 100%;
      height: 100%;
      transform: translateY(0);
    }
    img{
      height: 100%;
      width: auto;
    }
  }
  ul{
    list-style: none;
    list-style: none;
    z-index: 1;
    text-align: left;
  }
  li{
    color: #1F1F1F;
    font-family: Montserrat;
    font-size: 72px;    
    font-weight: 700;
    margin-bottom: 30px;  
    &:last-child { 
      margin-bottom: 0;  
    }
  }
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
    transform: translateY(0);
    transition: all 0.5s ease-in-out;
    &.out{
      transition: transform 0.3s ease-in-out;
      transform: translateY(-40vh);
    }
  }
  .box-btn{
    position: absolute;
    bottom: -78px;
    left: -126px;
    transition: opacity 0.6s ease-in-out, transform 0.3s ease-in-out;
    opacity: 0;    
    visibility: hidden;
    transform: translateY(0);
    &.out{
      transition: transform 0.3s ease-in-out;
      transform: translateY(26vh);
    }
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

.btn-back{
  position:fixed;
  top: 46px;
  left: 46px; 
  display: flex;
  gap: 5px;
  align-items: center;
  justify-content: center;
  color: #2D2D2D;  
  font-size: 20px;
  font-weight: 500;
  svg{
    width: 20px;
    height: auto;
  }
}

.fade-leave-active {
  transition: opacity 0.6s ease-in-out 0.4s;
}

.fade-enter-active{
  transition: opacity 0.6s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
