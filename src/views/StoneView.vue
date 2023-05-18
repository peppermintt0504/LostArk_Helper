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

      function resetStone (){
        buffAct1.value = Array(10).fill(0);
        buffAct2.value = Array(10).fill(0);
        debuffAct.value = Array(10).fill(0);

        percentage.value = 75;

        firstBuffCount.value = 0
        secendBuffCount.value = 0
        deBuffCount.value = 0
      }

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
            buff1.value = (buff1.value+1 === buff2.value? buff1.value + 2 : buff1.value + 1) % buffList.length;
            break;
          }
          case 2 : {
            buff2.value = (buff1.value === buff2.value+1? buff2.value + 2 : buff2.value + 1) % buffList.length;
            break;
          }
          case 3 : {
            debuff.value = (debuff.value + 1) % debuffList.length;
            break;
          }
        }
      }

      function setBuff (index,val){
        console.log('setbuff',index,val);
        switch (index) {
          case 1 : {
            buff1.value = val.target.value;
            break;
          }
          case 2 : {
            buff2.value = val.target.value;
            break;
          }
          case 3 : {
            debuff.value = val.target.value;
            break;
          }
        }
      }

      function getImageURL (name){
        return new URL(`../assets/ability/${name}.png`, import.meta.url).href
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
        setBuff,
        resetStone,
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
  <div class="pageLayout center blackColorLayout" oncopy="return false" oncut="return false" onpaste="return false">
    <div class="settingContainer">
      <button class="resetBTN" v-on:click="resetStone()">reset</button>
      <div class="buffSetting">
        <p class="settingTitle">증가 능력</p>
        <div class="buffSelectBox">
          <p>증가 능력 1 : </p>
          <select class="selectBox" @change="setBuff(1,$event)"  v-model="buff1">
            <option v-for="(buff,index) in buffList" :value="index">{{buff.replace(/_/g,' ')}}</option>
          </select>
        </div>
        
        <div class="buffSelectBox">
          <p>증가 능력 2 : </p>
          
          <select class="selectBox" @change="setBuff(2,$event)" v-model="buff2">
            <option v-for="(buff,index) in buffList" :value="index" v-if="(index !== buff1)">{{buff.replace(/_/g,' ')}}</option>
          </select>
        </div>
      </div>

      <div class="buffSetting">
        <p class="settingTitle">감소 능력</p>
        <div class="buffSelectBox">
          <p>감소 능력 1 : </p>
          <select class="selectBox" @change="setBuff(3,$event)"  v-model="debuff">
            <option v-for="(debuff,index) in debuffList" :value="index">{{debuff.replace(/_/g,' ')}}</option>
          </select>
        </div>
      </div>

      <div class="line"></div>

      <div class="buffSetting">
        <p class="settingTitle">목표 세공치</p>

        <div class="buffSelectBox">
          <p>증가 능력 1 : </p>
          <select class="selectBox">
            <option v-for="(count,index) in [0,1,2,3,4,5,6,7,8,9,10]" :value="count">{{count}}</option>
          </select>
        </div>
        
        <div class="buffSelectBox">
          <p>증가 능력 2 : </p>
          
          <select class="selectBox">
            <option v-for="(count,index) in [0,1,2,3,4,5,6,7,8,9,10]" :value="count">{{count}}</option>
          </select>
        </div>
      </div>      
    </div>
    <div class="stonePage">
      <img src="../assets/image/stoneScreen.png">
      <img class="debuffActive" :style="{display : (debuffAct[0] === 0 ? 'none' : '')}" src="../assets/image/감보석.png">
      <div class="debuffActiveCount" :style="{display : (debuffAct[0] === 0 ? 'none' : '')}">{{ debuffAct.reduce((x,v)=>v === 1?x+1:x,0) }}</div>

      <img class="buffFirstActive" :style="{display : (buffAct1[0] === 0 ? 'none' : '')}" src="../assets/image/보석.png">
      <div class="buffFirstActiveCount" :style="{display : (buffAct1[0] === 0 ? 'none' : '')}">{{ buffAct1.reduce((x,v)=>v === 1?x+1:x,0) }}</div>

      <img class="buffSecendActive" :style="{display : (buffAct2[0] === 0 ? 'none' : '')}" src="../assets/image/보석.png">
      <div class="buffSecendActiveCount" :style="{display : (buffAct2[0] === 0 ? 'none' : '')}">{{ buffAct2.reduce((x,v)=>v === 1?x+1:x,0) }}</div>

      <img v-on:click="changebuff(1)" class="buffFirst" :src="getImageURL(buffList[buff1])">

      <div class="buffFirstText">{{ buffList[buff1].replace(/_/g,' ') }}</div>

      <img v-on:click="changebuff(2)" class="buffSecend" :src="getImageURL(buffList[buff2])">

      <div class="buffSecendText">{{ buffList[buff2].replace(/_/g,' ') }}</div>
      

      <img v-on:click="changebuff(3)" class="debuff" :src="getImageURL(debuffList[debuff])">

      <div class="debuffText">{{ debuffList[debuff].replace(/_/g,' ') }}</div>

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
.blackColorLayout{
  background-color: #090a0b;
  justify-content: space-evenly;
}
.settingContainer{
  width: 300px;
  height: 100%;
  border : 1px solid rgb(54, 54, 54);
  border-radius: 5px;
}
.line{
  min-width: 80%;
  margin : 10px 10px;
  min-height: 1px;
  border-bottom: 1px solid gray;
}
.resetBTN{
  position: absolute;
  right: 20px;
  top : 25px;
}
.buffSetting{
  margin : 20px 15px;
}
.selectBox{
  height: 30px;
  width : 170px;
  border-radius: 7px;
}
.buffSelectBox{
  margin-top: 10px;
  width: 100%;
  height: 30px;
  display: flex;
  flex-direction: row;
  gap : 10px;
  align-items: center;
}
.settingTitle{
  font-size: 20px;
  font-weight: 700;
}
.stonePage{
  position: relative;
  border : 1px solid rgb(54, 54, 54);
  border-radius: 10px;
}
.twinkle{
  position: absolute;
  top : 255px;
  right: 35px;
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
  left: 28px;
  top: 276px;
  width: 55px;
  height: 55px;
}
.buffFirstText{
  position: absolute;
  left: 110px;
  top: 268px;
  font-size: 15px;
  color : #98c4e1;
  filter : blur(0.5px);
  text-shadow : 1px 1px 3px black;
  letter-spacing: -1px;
}
.buffSecend{
  position: absolute;
  left: 27px;
  top: 370px;
  width: 55px;
  height: 55px;
}
.buffSecendText{
  position: absolute;
  left: 110px;
  top: 361px;
  font-size: 15px;
  color : #98c4e1;
  filter : blur(0.5px);
  text-shadow : 1px 1px 3px black;
  letter-spacing: -1px;
}
.debuff{
  position: absolute;
  left: 28px;
  top: 497px;
  width: 55px;
  height: 55px;
}
.debuffText{
  position: absolute;
  left: 110px;
  top: 489px;
  font-size: 15px;
  color : #a03e3a;
  filter : blur(0.5px);
  text-shadow : 1px 1px 3px black;
  letter-spacing: -1px;
  font-weight: 600;
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
.firstButton:hover{
  background-color: black;
  opacity: 0.2;
}
.firstButton:active{
  background-color: black;
  opacity: 0.4;
}
.secendButton{
  position: absolute;
  right: 26px;
  top: 365px;
  opacity: 0.3;
  width: 92px;
  height: 65px;
}
.secendButton:hover{
  background-color: black;
  opacity: 0.2;
}
.secendButton:active{
  background-color: black;
  opacity: 0.4;
}
.debufButton{
  position: absolute;
  right: 26px;
  top: 492px;
  opacity: 0.3;
  width: 92px;
  height: 65px;
}
.debufButton:hover{
  background-color: black;
  opacity: 0.2;
}
.debufButton:active{
  background-color: black;
  opacity: 0.4;
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
