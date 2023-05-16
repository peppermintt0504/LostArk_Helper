<script setup>


</script>

<template>
  <main class="pageLayout">
    <div class="Title center">
      <span class="TitleFont">LoaHelper</span>
    </div>
    <div class="contentContainer center">
      <div class="contentFirstRow">
        
        <div class="firstContent">
          <div class="contentDescription">
            <p class="contentTitle">어빌리티 스톤 제련</p>
            <span class="contentDetail">어빌리티 스톤이 목표 세공 수치를 달성하기 위한 최선의 선택을 도와줍니다.</span>
          </div>
        </div>
        <div class="secondContent">
          <div class="contentDescription">
            <p class="contentTitle">어빌리티 스톤 제련</p>
            <span class="contentDetail">어빌리티 스톤이 목표 세공 수치를 달성하기 위한 최선의 선택을 도와줍니다.</span>
          </div>
        </div>

      </div>
      <div class="contentSecondRow">
        <div class="thirdContent">
          <div class="contentDescription">
            <p class="contentTitle">어빌리티 스톤 제련</p>
            <span class="contentDetail">어빌리티 스톤이 목표 세공 수치를 달성하기 위한 최선의 선택을 도와줍니다.</span>
          </div>
        </div>
        <div class="fourthContent">
          <div class="contentDescription">
            <p class="contentTitle">어빌리티 스톤 제련</p>
            <span class="contentDetail">어빌리티 스톤이 목표 세공 수치를 달성하기 위한 최선의 선택을 도와줍니다.</span>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
.Title{
  height: 300px;
  width: 100%;
  background-color: #7b9acc;
}
.TitleFont{
  font-size: 30px;
  font-weight: 700;
}
.contentContainer{
  height: calc(100vh - 350px);
  width: 100%;
  background-color: var(--vt-c-middleWhite);

}
.contentFirstRow{
  height: 100%;
  width   : 50%;
  position: relative;
  z-index : 1;
  color : var(--vt-c-bule);
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}
.contentFirstRow::before{
  content : "";
  position: absolute;
  right   : -10%;
  bottom  : 50%;
  height  : 1px;
  width   : 20%;  /* or 100px */
  border-bottom:1px solid var(--vt-c-bule);
}
.contentSecondRow{
  height: 100%;
  width   : 50%;
  position: relative;
  z-index : 1;
  color : var(--vt-c-bule);
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}
.contentSecondRow::before{
  content : "";
  position: absolute;
  bottom  : 40%;
  height  : 20%;
  width   : 1px;  /* or 100px */
  border-left:1px solid var(--vt-c-bule);
}
.firstContent{
  display: flex;
  justify-content: end;
  margin-right: 10%;
}
.secondContent{
  display: flex;
  justify-content: end;
  margin-right: 10%;
}
.thirdContent{
  display: flex;
  justify-content: start;
  margin-left: 10%;
}
.fourthContent{
  display: flex;
  justify-content: start;
  margin-left: 10%;
}
.contentTitle{
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 5px;
}
.contentDetail{
  font-size: 13px;
}
.contentDescription{
  width: 200px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  border : 1px solid rgba(106, 134, 138, 0.404);
  border-radius: 10px;
  padding: 10px;
  box-shadow: 1px 3px 3px 1px rgba(0, 0, 0, 0.082);
}
</style>