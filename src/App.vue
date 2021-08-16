<template>
  <div
    id="app"
    class="container"
  >
    <router-view />
    <div class="bg__container">
      <div class="animater" />
      <div class="grass" />
    </div>
  </div>
</template>

<style scoped lang="scss">
@import './assets/scss/main.scss';
#app {
  background:linear-gradient(0deg, rgba(162,220,246,1) 9%, rgba(111,217,249,1) 80%, rgba(58,202,245,1) 100%);
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
  .bg__container{
    width: 100%;
    height: 180px;
    display: flex;
    .animater, .grass{
      display: none;
    }
  }
}
@media screen and(min-width:480px) {
  #app {
  background:linear-gradient(0deg, rgba(162,220,246,1) 9%, rgba(111,217,249,1) 80%, rgba(58,202,245,1) 100%);
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
  .bg__container{
    width: 100%;
    height: 180px;
    display: flex;
    .animater, .grass{
      display: block;
    }
    .animater{
      background-image: url('https://i.imgur.com/OW3IUzW.png');
      background-size: 180px;
      height: 180px;
      width: 180px;
      position: absolute;
      bottom: 0;
      right: 5%;
      background-repeat: no-repeat;
      background-position: 0 0;
      margin-bottom: 5px;
      animation:  alpaca 1s linear infinite;
      z-index: 0;
    }
    .grass{
      background-image: url('https://i.imgur.com/2JCPPrD.png');
      height: 70px;
      z-index: 2;
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      background-repeat: repeat-x;
      background-position: 0 0;
      animation: grass 15s linear infinite;
    }
  }
}
}
@keyframes grass{
  from{
    background-position-x:0;
  }
 100%{
    background-position-x: -1198px;
  }
}
@keyframes alpaca {
  0%{
    transform: translateY(0);
  }
  50%{
    transform: translateY(1rem);
  }
  100%{
    transform: translateY(0);
  }

}

</style>
