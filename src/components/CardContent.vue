<script >
import Elbows from '../assets/Elbows.vue'

export default {
  components:{
    Elbows
  },  
  props: {      
    title:{
        type: String,
        default: ''
    },
    rightElbows:{
      type: Boolean,
      default: false
    },
    leftElbows:{
      type: Boolean,
      default: false
    },
    animate:{
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      
    };
  }, 
    
};
</script>

<template>
  <div class="card-content">
    <div v-if="leftElbows" class="elbows-top" :class="{in : animate === true}">
      <Elbows/>
    </div>
    <div v-if="rightElbows" class="elbows-bottom" :class="{in : animate === true}">
      <Elbows/>
    </div>
    <div class="wrap-content" :class="{in : animate === true}">
      <div class="content-title" v-if="title.length !== 0">
        {{ title }}
      </div>
      <div class="content-desc">
        <slot></slot>
      </div>
    </div>    
  </div>
     
</template>

<style lang="scss" scoped>
.card-content{
  margin: 40px;
  position: relative;
}
.wrap-content{
  border-radius: 10px;
  background: #FFFFFF80;
  box-shadow: 5px 5px 20px 0px #00000026;
  padding: 30px 40px;
  max-width: 581px;
  position: relative;
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 30px;
  height: fit-content;
  width: auto;
  transform: scale(0);
  transition: all 0.4s ease-in-out;
  &.in{
    transform: scale(1);
  }
}
.content-title{  
  font-size: 64px;
  font-weight: 700;
  line-height: 78px;
  letter-spacing: 0em;  
}
.content-desc{  
  font-size: 36px;
  font-weight: 600;
  line-height: 44px;
  letter-spacing: 0em;  
}

.elbows-top{
  position:absolute;
  top: -40px;
  left: -40px;
  svg{
    width: 0;
    height: 0;
  }
}

.elbows-bottom{
  position:absolute;
  bottom: -40px;
  right: -40px;  
  svg{
    transform: rotate(180deg);
    width: 0;
    height: 0;
  }
}

.elbows-bottom, .elbows-top{  
  svg{
    transition: all 0.4s ease;
  }
  &.in{
    svg{
      width: 100px !important;
      height: 100px !important;
    }
  }
}
</style>
