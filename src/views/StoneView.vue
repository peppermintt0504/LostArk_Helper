<script>
  import buffList from '../enum/buff';
  import debuffList from '../enum/debuff';
  import { ref } from 'vue';
  export default {
    props: {
    },
    setup(){
      const buffAct1 = ref(Array(10).fill(0));
      const buffAct2 = ref(Array(10).fill(0));
      const debuffAct = ref(Array(10).fill(0));

      let percentage = ref(75);

      let buff1 = ref(0);
      let buff2 = ref(1);
      let debuff = ref(0);

      let effect = ref(false);

      let firstBuffCount = ref(0);
      let secendBuffCount = ref(0);
      let deBuffCount = ref(0);

      function tryWork (type) {
        if(type === 'first' && firstBuffCount.value === 10) return;
        if(type === 'secend' && secendBuffCount.value === 10) return;
        if(type === 'debuff' && deBuffCount.value === 10) return;
        
        effect.value = true;
        setTimeout(()=>{effect.value = false;},300);

        const result = parseInt(Math.random()*100);
        let workResult = false;
        if(result <= percentage.value){
          percentage.value = percentage.value === 25 ? 25 :percentage.value - 10;
          workResult = true;
        }else{
          percentage.value = percentage.value === 75 ? 75 :percentage.value + 10;
        }

        switch (type) {
          case 'first' : {
            if(workResult){
              buffAct1.value[firstBuffCount.value] = 1;
            }else{
              buffAct1.value[firstBuffCount.value] = 2;
            }
            firstBuffCount.value++;
            break;
          }
          case 'secend' : {
            if(workResult){
              buffAct2.value[secendBuffCount.value] = 1;
            }else{
              buffAct2.value[secendBuffCount.value] = 2;
            }
            secendBuffCount.value++;
            break;
          }
          case 'debuff' : {
            if(workResult){
              debuffAct.value[deBuffCount.value] = 1;
            }else{
              debuffAct.value[deBuffCount.value] = 2;
            }
            deBuffCount.value++;
            break;
          }
        }
      }

      function changebuff (index){
        switch (index) {
          case 1 : {
            buff1.value = (buff1.value + 1) % buffList.length;
            break;
          }
          case 2 : {
            buff2.value = (buff2.value + 1) % buffList.length;
            break;
          }
          case 3 : {
            debuff.value = (debuff.value + 1) % debuffList.length;
            break;
          }
        }
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
        tryWork,
        percentage,
        debuffList,
        buffList,
        buffAct1,
        buffAct2,
        debuffAct,
        debuff,
        buff1,
        buff2,
        effect,
      }
    }
  }
</script>

<template>
  <div class="pageLayout center" oncopy="return false" oncut="return false" onpaste="return false">
    <div class="stonePage">
      <img src="../assets/image/stoneScreen.png">
      <img class="debuffActive" :style="{display : (debuffAct[0] === 0 ? 'none' : '')}" src="../assets/image/감보석.png">
      <div class="debuffActiveCount" :style="{display : (debuffAct[0] === 0 ? 'none' : '')}">{{ debuffAct.reduce((x,v)=>v === 1?x+1:x,0) }}</div>

      <img class="buffFirstActive" :style="{display : (buffAct1[0] === 0 ? 'none' : '')}" src="../assets/image/보석.png">
      <div class="buffFirstActiveCount" :style="{display : (buffAct1[0] === 0 ? 'none' : '')}">{{ buffAct1.reduce((x,v)=>v === 1?x+1:x,0) }}</div>

      <img class="buffSecendActive" :style="{display : (buffAct2[0] === 0 ? 'none' : '')}" src="../assets/image/보석.png">
      <div class="buffSecendActiveCount" :style="{display : (buffAct2[0] === 0 ? 'none' : '')}">{{ buffAct2.reduce((x,v)=>v === 1?x+1:x,0) }}</div>

      <img v-on:click="changebuff(1)" class="buffFirst" :src="getImageURL(buffList[buff1])">
      <img class="buffFirstText" :src="getTextURL(buffList[buff1])">
      <img v-on:click="changebuff(2)" class="buffSecend" :src="getImageURL(buffList[buff2])">
      <img class="buffSecendText" :src="getTextURL(buffList[buff2])">
      <img v-on:click="changebuff(3)" class="debuff" :src="getImageURL(debuffList[debuff])">
      <img class="debuffText" :src="getTextURL(debuffList[debuff])">
      <img v-for="(buff,index) in buffAct1" class="buffFirstActiveStone" :style="{ left : `${109 + (40 * index)}px`,display : (buff === 0 ? 'none' : '') }" :src="activeURL(buff === 1 ? 'active' : 'fail')">
      <img v-for="(buff,index) in buffAct2" class="buffSecendActiveStone" :style="{ left : `${109 + (40 * index)}px`,display : (buff === 0 ? 'none' : '') }" :src="activeURL(buff === 1 ? 'active' : 'fail')">
      <img v-for="(buff,index) in debuffAct" class="debuffActiveStone" :style="{ left : `${109 + (40 * index)}px`,display : (buff === 0 ? 'none' : '') }" :src="activeURL(buff === 1 ? 'active' : 'fail')">
      <div class="firstButton" v-on:click="tryWork('first')"></div>
      <div class="secendButton" v-on:click="tryWork('secend')"></div>
      <div class="debufButton" v-on:click="tryWork('debuff')"></div>
      
      
      <div class="buffFirstpercentage">
        <span class="percentageText">성공 확률 </span>
        <span class="percentage">{{percentage}}</span>
        <span class="percentageEnd">%</span>
      </div>
      <div class="debuffpercentage">
        <span class="percentageText">균열 확률 </span>
        <span class="percentage">{{percentage}}</span>
        <span class="percentageEnd">%</span>
      </div>

      <div class="twinkle" :style="{backgroundColor : (effect ? '#fffe8c' : '#0000'), boxShadow : (effect ? '0px 0px 15px 15px #fffe8c' : '')}"></div>
    </div>
  </div>
</template>

<style>
*{-webkit-user-drag: none;}
.stonePage{
  height: 100%;
  position: relative;
}
.twinkle{
  position: absolute;
  top : 255px;
  right: 40px;
  width: 15px;
  height: 0px;
  background-color: #fffe8c;
  transition: box-shadow 0.5s,background-color 0.2s;
  /* filter: drop-shadow(0 0 2px rgba(36, 255, 102, 0.7)) */
  /* box-shadow: 0px 0px 15px 15px #fffe8c; */
}
.debuffActive{
  position: absolute;
  right: 123px;
  top: 489.5px;
}
.debuffActiveCount{
  position: absolute;
  right: 142px;
  top: 489px;
  color : #af4440;
  filter: blur(0.5px);
}
.buffFirstActiveCount{
  position: absolute;
  right: 142px;
  top: 268px;
  color : #01acf3;
  filter: blur(0.5px);
}
.buffSecendActiveCount{
  position: absolute;
  right: 142px;
  top: 362px;
  color : #01acf3;
  filter: blur(0.5px);
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
.debuff{
  position: absolute;
  left: 13px;
  top: 484px;
}
.debuffText{
  position: absolute;
  left: 102px;
  top: 488.5px;
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
.debuffActiveStone{
  position: absolute;
  top: 514px;
  left: 109px;
}
.firstButton{
  position: absolute;
  right: 26px;
  top: 273px;
  opacity: 0.3;
  width: 92px;
  height: 65px;
}
.secendButton{
  position: absolute;
  right: 26px;
  top: 365px;
  opacity: 0.3;
  width: 92px;
  height: 65px;
}
.debufButton{
  position: absolute;
  right: 26px;
  top: 492px;
  opacity: 0.3;
  width: 92px;
  height: 65px;
}
.buffFirstpercentage{
  position: absolute;
  top : 235px;
  right: 20px;
  filter: blur(0.5px);
}
.debuffpercentage{
  position: absolute;
  top : 455px;
  right: 20px;
  filter: blur(0.5px);
}
.percentageText{
  color : white;
  font-size: 15px;
}
.percentage{
  color : #d3ae04f2;
  font-size: 18px;
}
.percentageEnd{
  color : #d3ae04f2;
  font-size: 18px;
}
@media (min-width: 1024px) {
  
}
</style>
