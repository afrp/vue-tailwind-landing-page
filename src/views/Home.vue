<script >
import ArrowLeft from '../assets/ArrowLeft.vue'
import ArrowBack from '../assets/ArrowBack.vue'
import TriangglePlay from '../assets/TriangglePlay.vue'
import CardContent from '../components/CardContent.vue'

export default {
  components:{
    ArrowLeft,
    ArrowBack,
    TriangglePlay,
    CardContent
  },  
  data() {
      return {
        page: 1,
        activeMenu: 1, // 1: About Us, 2: Our Product, 3: Contact Us
        lateAnim: false,
        form:{
          name:'',
          email: '',
        },
        carousel: true,
        listShow: false,
        carouselData: ['We Solve Your', 'We Know You Have', 'We Solve Your'],
        bgPage2:[
          {
            img: '/bg-menu-1.png',
            alt: 'About us'
          },
          {
            img: '/bg-menu-2.png',
            alt: 'Our Product'
          },
          {
            img: '/bg-menu-3.png',
            alt: 'Contact us'
          },
        ]        
      };
  },
  computed:{
    bgTransition(){
      if (this.activeMenu === 2){
        return "transform: translateY(-33.333333333%);"
      } else if (this.activeMenu === 3){
        return "transform: translateY(-66.666666666%);"
      } else {
        return ""
      }
    }   
  },
  methods:{
    lateAnimate(){
      this.lateAnim = false;
      setTimeout(() => {
          this.lateAnim = true;
      }, 1000);
    },
    slideCarousel(){
      this.$refs.page2.scrollBy({
          left: this.carousel ? 580 : -580,
          behavior: 'smooth'
      });
      this.carousel = !this.carousel;
    }
  }  
};
</script>

<template>
  <div class="container flex">
    <div class="line-one top" :class="{'active-one' : listShow === true}"></div>
    <div class="line-two top second" :class="{'active-two' : listShow === true}"></div>
    <div class="line-one bottom" :class="{'active-one' : listShow === true}"></div>
    <div class="line-two bottom second" :class="{'active-two' : listShow === true}"></div>
    <div class="page-wrap" :class="{'to-left': page === 2}">
      <transition name="fade" mode="out-in">
        <div v-show="page === 1" class="card-intro" @mouseover="listShow = true" @mouseleave="listShow = false">          
          <div class="flex justify-center items-center w-full h-full overflow-hidden">
            <img                                        
                src="/image-intro.png"
                alt="Image intro"
                class="intro-img"
            />
          </div>
          <div class="title-intro" :class="{out: page === 2}">We Create</div>
          <div class="box-btn" :class="{out: page === 2}">      
            <div class="btn-intro" role="button" @click="page = 2;lateAnimate();">
              <div class="bg-btn" />
              <span>AWESOME THINGS</span>
              <ArrowLeft />
            </div>
          </div>
        </div>                
      </transition>
      <div v-show="page === 2" class="bg-menu-list" :class="{in: lateAnim === true}"></div>
      <div class="card-menu" :class="{'show': page === 2}">
        <div class="wrap-menu">
          <div class="bg-menu-image">
            <div class="flex flex-col img-wrap" :style="bgTransition">
              <img 
                v-for="(data, index) in bgPage2"
                :key="index"
                :src="data.img" 
                :style="[lateAnim ? {filter: 'grayscale(100%)'} : {}]" 
                :alt="data.alt"
              />              
            </div>
            <!-- <div class="overlay" :class="{in: lateAnim === true}"></div> -->
          </div>
          <ul>
            <li role="button" class="list-menu" :class="{'active' : activeMenu === 1}" @click="activeMenu = 1; lateAnimate()">About Us</li>
            <li role="button" class="list-menu" :class="{'active' : activeMenu === 2}" @click="activeMenu = 2; lateAnimate()">Our Product</li>
            <li role="button" class="list-menu" :class="{'active' : activeMenu === 3}" @click="activeMenu = 3; lateAnimate()">Contact Us</li>
          </ul>
          <div v-show="activeMenu === 1" class="content-page">
            <CardContent title="Our People Come First" leftElbows :animate="lateAnim">
              We are independently owned, strategic creative agency forever curious and ready to transform the way business is done.
            </CardContent>
            <button type="button" class="my-btn btn-content" :class="{in: lateAnim === true}" @click="lateAnimate">Learn more</button>
          </div>
          <transition name="fade-back" mode="out-in">
            <div v-show="activeMenu === 2 && lateAnim" ref="page2" class="content-page page-two">
              <div class="relative w-full h-full">
                <div class="wrap-carousel">
                  <CardContent                     
                    v-for="(data,index) in carouselData"
                    :key="index" 
                    :title="data"
                    class="card-carousel"
                  >
                    <div class="text-carousel">PROBLEM</div>
                  </CardContent>                  
                </div>              
              </div>            
            </div>
          </transition>
          <transition name="fade-back" mode="out-in">
            <div class="btn-play" v-show="activeMenu === 2 && lateAnim" role="button" @click="slideCarousel">
              <TriangglePlay />
            </div>
          </transition>          
          <div v-show="activeMenu === 3" class="content-page">
            <CardContent leftElbows rightElbows :animate="lateAnim">
              <div class="form-content">
                <div class="form-group">
                    <label for="inputName" class="form-label">Type your beautiful name</label>
                    <input id="inputName" v-model="form.name" type="text" class="form-control" placeholder="in here of course :)">
                </div>
                <div class="form-group">
                    <label for="inputEmail" class="form-label">Protect your email address</label>
                    <input id="inputEmail" v-model="form.email" type="text" class="form-control" placeholder="but not in here :)">
                </div>
                <button type="button" class="my-btn w-full" style="height: 73px;" @click="lateAnimate">Learn more</button>
              </div>              
            </CardContent>            
          </div>          
        </div>        
      </div>
      <transition name="fade" mode="out-in">
      <div 
        class="btn-back" 
        :style="[lateAnim ? {color: '#FFFFFF'} : {color: '#2D2D2D'}]"
        v-if="page === 2" 
        @click="page = 1;" 
        role="button"
      >
        <ArrowBack/>
        <span>Back</span>
      </div>
      </transition>
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
    .line-one, .line-two{
      position: absolute;    
      height: 18px;
      background: #FFB800;
      width: 0;
      transition: all 0.4s ease-in-out;
      &.active-two{
        width: 140px;
      }
      &.active-one{
        width: 67px;
      }
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
}
.page-wrap{  
  position: relative;
  width: 961px;
  height: 598px;
  min-height: 598px;
  margin: auto calc(50% - 480.5px) auto auto;
  transition: all 0.3s ease-in-out;  
  &.to-left{
    transition: all 0.3s ease-in-out 0.4s;
    margin: auto 0 auto auto;    
    width: 968px;
    height: 100vh;
    min-height: 1024px;
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
      transform: translateY(50vh);
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
      left: -85vw;
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
      &.out{      
        transform: translateY(50vh);
      }
    }
    .btn-intro{      
      span, svg{
        transform: translateX(0);
      }
    }    
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
.bg-menu-list{
  width: 0;
  height: 288px;
  background: #FFB800;
  position: fixed;
  top: 0;
  left: 0;
  transition: width 0.4s ease-in-out;
  &.in{
    width: calc(100vw - 960px);
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
      height: max-content;
      transform: translateY(0);
      transition: transform 0.3s ease-in-out;
    }
    img{
      height: 100vh;
      min-height: 1024px;
      width: auto;
      filter: grayscale(0);    
      transition: all 0.5s ease-in-out;
    }    
    .overlay{
      width:100%;
      height:100%;      
      position:absolute;
      top:0;
      left:-100%;
      background-color: rgb(76 75 75 / 68%);      
      background-size: 100%;
      background-blend-mode: saturation;
      transition: left 0.4s ease-in-out;
      &.in{
        left:0;
      }
    }
  }
  ul{
    list-style: none;
    list-style: none;
    z-index: 1;
    text-align: left;
    position: absolute;
    top: 55%;
    left: -200px;
  }
  .list-menu{
    color: #1F1F1F;
    font-family: Montserrat;
    font-size: 72px;    
    font-weight: 700;
    margin-bottom: 30px;  
    position: relative;

    &:last-child { 
      margin-bottom: 0;  
    }
    &:hover{
      opacity: 0.6;
    }
    &::after{         
      content: "";      
      width: 0;
      height: 17px;        
      position: absolute;
      background: #FFB800;
      left: -173px;
      top: 50%;
      transform: translateY(-50%);
      transition: width 0.3s ease;
    }
    &.active{
      color: #FFB800;
      &:hover{
        opacity: 1;
      }
      &::after{                 
        width: 128px;
      }
    }    
  }
  .content-page{    
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 50%;
    right: 13px;
    transform: translateY(-50%);
    z-index: 1;
    &.page-two{
      right: 0;      
      overflow-x: hidden;
      width: 620px;
      height: fit-content;
        
      .wrap-carousel{
        display: flex;
        gap: 40px;
        width: fit-content;        
      }        
      .text-carousel{
        background-image: -webkit-linear-gradient(left, white 50%, #FFB800 50%);
        background-repeat: repeat;
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        -webkit-animation: stripes 2s linear infinite;
        animation: stripes 2s linear infinite;
        background-size: 200% 100%;
        background-position: 100%;
        font-family: Montserrat;
        font-size: 64px;
        font-weight: 700;
        line-height: 78px;
      }    
    }
    button{
      margin-left: auto;
      margin-right: 40px;
    }
    .btn-content{
      transform: translateY(40vh);
      transition: all 0.4s ease-in-out;
      &.in{
        transform: translateY(0);
      }
    }
  }

  .btn-play{
      position: absolute;
      right: 30px;
      top: 50%;
      transform: translateY(-50%);
      width: 108px;
      height: 108px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #FFB800;
      color: #FFFFFF;
      z-index: 1;
      svg{
        width: 49px;
        height: auto;
      }
    }
  .form-content{
    width: 448px;
    display: flex;
    flex-direction: column;
    gap: 25px;
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

@keyframes stripes {
  100% {
    background-position: 385px 0;
  }
}

.fade-back-leave-active, .fade-back-enter-active {
  transition: all 0.4s ease;
}
.fade-back-enter-from, .fade-back-leave-to {
  opacity: 0;
}
</style>
