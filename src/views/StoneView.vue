<script>
  import buffList from '../enum/buff';
  import { ref } from 'vue';
  export default {
    props: {
    },
    data () {
      return {

        buffAct1 : [0,1,1,0,1,0,1,1,1,1],
        buffAct2 : [0,1,0,1,1,0,1,0,1,1],
        
      }
    },
    setup(){
      let buff1 = ref(0);
      let buff2 = ref(0);
      function changebuff (index){
        index === 1 ? buff1.value = (buff1.value + 1) % buffList.length : buff2.value = (buff2.value + 1) % buffList.length;
      }
      function getImageURL (name){
        return new URL(`../assets/image/${name}.png`, import.meta.url).href
      }
      function getTextURL (name){
        return new URL(`../assets/image/${name}_텍스트.png`, import.meta.url).href
      }
      function activeURL (active){
        return new URL(`../assets/image/${active}.png`, import.meta.url).href
      }
      return {
        getImageURL,
        getTextURL,
        activeURL,
        changebuff,
        buffList,
        buff1,
        buff2
      }
    }
  }
</script>

<template>
  <div class="pageLayout center">
    <div class="stonePage">
      <img src="../assets/image/stoneScreen.png">
      <!-- <img class="debuffActive" src="../assets/image/감보석.png">
      <img class="buffFirstActive" src="../assets/image/보석.png">
      <img class="buffSecendActive" src="../assets/image/보석.png"> -->
      <img v-on:click="changebuff(1)" class="buffFirst" :src="getImageURL(buffList[buff1])">
      <img class="buffFirstText" :src="getTextURL(buffList[buff1])">
      <img v-on:click="changebuff(2)" class="buffSecend" :src="getImageURL(buffList[buff2])">
      <img class="buffSecendText" :src="getTextURL(buffList[buff2])">
      <img v-for="(buff,index) in buffAct1" class="buffFirstActiveStone" :style="{ left : `${109 + (40 * index)}px` }" :src="activeURL(buff ? 'active' : 'fail')">
      <img v-for="(buff,index) in buffAct2" class="buffSecendActiveStone" :style="{ left : `${109 + (40 * index)}px` }" :src="activeURL(buff ? 'active' : 'fail')">
    </div>
  </div>
</template>

<style>
.stonePage{
  height: 100%;
  position: relative;
}
.debuffActive{
  position: absolute;
  right: 123px;
  bottom: 217px;
}
.buffFirstActive{
  position: absolute;
  right: 123px;
  bottom: 437px;
}
.buffSecendActive{
  position: absolute;
  right: 123px;
  bottom: 344px;
}
.buffFirst{
  position: absolute;
  left: 13px;
  top: 262px;
}
.buffFirstText{
  position: absolute;
  left: 104px;
  top: 268px;
}
.buffSecend{
  position: absolute;
  left: 12px;
  top: 356px;
}
.buffSecendText{
  position: absolute;
  left: 104px;
  top: 361px;
}
.buffFirstActiveStone{
  position: absolute;
  top: 294px;
  left: 109px;
}
.buffSecendActiveStone{
  position: absolute;
  top: 387px;
  left: 109px;
}
@media (min-width: 1024px) {
  
}
</style>
