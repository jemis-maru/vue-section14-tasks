<template>
  <router-view v-slot="slotProps">
    <transition name="route" mode="out-in">
      <component :is="slotProps.Component"></component>
    </transition>
  </router-view>
  <!-- <div class="container">
    <list-data></list-data>
  </div>
  <div class="container">
    <div class="block" :class="{animate: animateBlock}"></div>
    <button @click="animateBlockFun">Animate</button>
  </div>
  <div class="container">
    <transition name="para"
      :css="false"
      @before-enter="beforeEnterFun"
      @enter="enterFun"
      @after-enter="afterEnterFun"
      @before-leave="beforeLeaveFun"
      @leave="leaveFun"
      @after-leave="afterLeaveFun"
      @enter-cancelled="enterCancelFun"
      @leave-cancelled="leaveCancelFun">
      <p v-if="visiblePara">This is paragraph...</p>
    </transition>
    <button @click="toggleParaFun">Toggle Paragraph</button>
  </div>
  <div class="container">
    <transition name="userToggle" mode="out-in">
      <button @click="showUsersFun" v-if="!usersVisible">Show users</button>
      <button @click="hideUsersFun" v-else>Hide users</button>
    </transition>
  </div>
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div> -->
</template>  

<script>
// import ListData from './components/ListData.vue';

export default {
  // components: {
  //   'list-data': ListData,
  // },
  data() {
    return {
      dialogIsVisible: false,
      animateBlock: false,
      visiblePara: false,
      usersVisible: false,
      enterInterval: 0,
      leaveInterval: 0,
    };
  },
  methods: {
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateBlockFun(){
      this.animateBlock = true;
    },
    toggleParaFun(){
      this.visiblePara = !this.visiblePara;
    },
    showUsersFun(){
      this.usersVisible = true;
    },
    hideUsersFun(){
      this.usersVisible = false;
    },
    beforeEnterFun(ele){
      console.log('before enter called');
      ele.style.opacity = 0;
    },
    enterFun(ele, done){
      console.log('enter called');
      let count = 1;
      this.enterInterval = setInterval(() => {
        ele.style.opacity = (count * 0.1);
        count++;
        if(count>100){
          clearInterval(this.enterInterval);
          done();
        }
      }, 20);
    },
    afterEnterFun(ele){
      console.log(ele);
      console.log('after enter called');
    },
    beforeLeaveFun(ele){
      console.log('before leave called');
      ele.style.opacity = 1;
    },
    leaveFun(ele, done){
      console.log('leave called');
      let count = 1;
      this.leaveInterval = setInterval(() => {
        ele.style.opacity = 1 - (count * 0.1);
        count++;
        if(count>100){
          clearInterval(this.leaveInterval);
          done();
        }
      }, 20);
    },
    afterLeaveFun(ele){
      console.log(ele);
      console.log('after leave called');
    },
    enterCancelFun(ele){
      console.log(ele);
      clearInterval(this.enterInterval);
      console.log('enter cancelled called');
    },
    leaveCancelFun(ele){
      console.log(ele);
      clearInterval(this.leaveInterval);
      console.log('leave cancelled called');
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition: transform 0.3s ease-out; */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.animate {
  /* transform: translateX(-50px); */
  animation: slide-fade 0.3s ease-out forwards;
}
/* .para-enter-from, .para-leave-to{
  opacity: 0;
  transform: translateY(-30px);
}
.para-enter-active, .para-leave-active{
  transition: all 0.3s ease-out;
}
.para-enter-to, .para-leave-from{
  opacity: 1;
  transform: translateY(0px);
} */
.userToggle-enter-from, .userToggle-leave-to{
  opacity: 0;
}
.userToggle-enter-active, .userToggle-leave-active{
  transition: all 0.3s ease-out;
}
.userToggle-enter-to, .userToggle-leave-from{
  opacity: 1;
}
.route-enter-from, .route-leave-to{
  opacity: 0;
}
.route-enter-active, .route-leave-active{
  transition: all 1s ease-out;
}
.route-enter-to, .route-leave-from{
  opacity: 1;
}

@keyframes slide-fade {
  0% {
    transform: translateX(0px) scale(1);
  }
  70% {
    transform: translateX(-30px) scale(1.1);
  }
  100% {
    transform: translateX(-50px) scale(1);
  }
}
</style>