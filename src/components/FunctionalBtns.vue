<template>
  <button
    class="functional-btn"
    @click.stop.prevent="$emit('random-style')"
  >
    <img
      src="./../assets/icons/dices.svg"
      alt=""
    >
    Random
  </button>
  <button
    class="functional-btn"
    @click.stop.prevent="$emit('reset')"
  >
    Reset
  </button>
  <button
    class="functional-btn"
    @click.stop.prevent="$emit('downloadImg')"
  >
    <img
      src="./../assets/icons/download.svg"
      alt=""
    >Download
  </button>
</template>
<script>
export default {
  name: 'FunctionalBtn',
  emits: ['random-style', 'reset', 'downloadImg']
}
</script>

<style lang="scss" scoped>
@import '../assets/scss/main.scss';

.functional-btn{

  background: #fff;
  height: 40px;
  width: 100%;
  line-height: 40px;
  margin-right: 16px;
  display: flex;
  justify-content: center;
  font-size: 14px;
  &:hover{
    box-shadow: 1px 1px 5px 0px rgba(143,140,140,0.75);
    transition: box-shadow 0.2s ease-in;
  }
  img{
    margin: auto 10px auto 0;
    width: 20px;
    height: 20px;
  }
  &:first-child{
    position: fixed;
    bottom: 0;
    left: 0;
    font-size: 18px;
    height: 45px;
    line-height: 45px;
    box-shadow: 0px 0px 10px -1px rgb(0 0 0 / 5%);

    &:hover >img{
      transform: rotate(0.5turn);
      transition: transform 0.1s ease-in-out;
    }
  }
}
@media screen and (min-width: 480px){
  .functional-btn{
    &:first-child{
      position: static;
      grid-column: 1/3;
      margin-bottom: 16px;
      height: 40px;
      font-size: 14px;
      line-height: 40px;
      box-shadow: none
    }
  }
}

</style>
