<script setup lang="ts">
</script>

<template>
  <div class="pageLayout center">
    <div class="stonePage">
      <img src="../assets/image/stoneScreen.png">
      <!-- <img class="debuffActive" src="../assets/image/감보석.png">
      <img class="buffFirstActive" src="../assets/image/보석.png">
      <img class="buffSecendActive" src="../assets/image/보석.png"> -->
      <img class="buffFirst" src="../assets/image/선수필승.png">
      <img class="buffFirstText" src="../assets/image/선수필승_텍스트.png">
      <img class="buffSecend" src="../assets/image/실드_관통.png">
      <img class="buffSecendText" src="../assets/image/실드_관통_텍스트.png">
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
  bottom: 384px;
}
.buffFirstText{
  position: absolute;
  left: 104px;
  bottom: 437px;
}
.buffSecend{
  position: absolute;
  left: 13px;
  bottom: 291px;
}
.buffSecendText{
  position: absolute;
  left: 104px;
  bottom: 345px;
}
@media (min-width: 1024px) {
  
}
</style>
