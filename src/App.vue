<template>
  <div
    id="app"
    class="container"
  >
    <router-view />
    <div class="bg__container">
      <div class="animater" />
      <div class="glass" />
    </div>
  </div>
</template>

<style scoped lang="scss">
@import './assets/scss/main.scss';
#app {
  background-color: #EEECEE;
  width: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  .bg__container{
    width: 100%;
    height: 180px;
    display: flex;
    .animater{
      background-image: url('https://i.imgur.com/OW3IUzW.png');
      background-size: 200px;
      height: 200px;
      width: 200px;
      position: absolute;
      bottom: 0;
      left: 75%;
      background-repeat: no-repeat;
      background-position: 0 0;
      margin-bottom: 5px;
      animation:  alpaca 1s linear infinite;
      z-index: 0;
    }
    .glass{
      background-image: url('https://i.imgur.com/BCTNSdz.png');
      height: 70px;
      width: 1000%;
      z-index: 2;
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      animation: glass 15s linear infinite;
      background-repeat: repeat-x;
    }
  }
}
@keyframes glass{
  from {
    transform: translateX(0)
  } to {
    transform: translateX(-1800px)
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
