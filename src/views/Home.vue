<template>
  <div class="main__container">
    <h1>ALPACA GENERATOR</h1>
    <div class="interaction">
      <div class="interaction__left-content">
        <div class="interaction__left-content__image-wrapper">
          <div class="interaction__left-content__image-wrapper__bg">
            <img
              src="./../assets/images/backgrounds/blue50.png"
              alt=""
            >
          </div>
          <div class="interaction__left-content__image-wrapper__body">
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/ears/default.png"
                alt=""
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/hair/default.png"
                alt=""
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/leg/default.png"
                alt=""
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/mouth/default.png"
                alt=""
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/neck/default.png"
                alt=""
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/nose.png"
                alt=""
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                src="./../assets/images/eyes/default.png"
                alt=""
              >
            </div>
          </div>
          <div class="interaction__left-content__image-wrapper__decoration" />
        </div>
        <div class="interaction__left-content__btn-wrapper">
          <button>Random</button>
          <button>Download</button>
        </div>
      </div>
      <div class="interaction__select-wrapper">
        <div class="interaction__select-wrapper__category">
          <div class="interaction__select-wrapper__category__title">
            ACCESSORIZE THE ALPACA'S
          </div>
          <div class="interaction__select-wrapper__category__item">
            <button
              v-for="category in categories"
              :key="categories.indexOf(category)"
              class="circle-btn"
            >
              {{ category }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'Home',
  data () {
    return {
      categories: ['Hair', 'Ears', 'Eyes', 'Leg', 'Mouth', 'Neck', 'Backgroundss'],
      decorations: {
        Hair: ['bang', 'curls', 'elegant', 'fancy', 'quiff', 'short'],
        Ears: ['tilt-backward', 'tilt-forward'],
        Eyes: ['angry', 'naughty', 'panda', 'smart', 'star'],
        Leg: ['bubble-tea', 'cookie', 'game-console', 'tilt-backward', 'tilt-forward'],
        Mouth: ['astonished', 'eating', 'laugh', 'tongue'],
        Neck: ['bend-backward', 'bend-forward', 'thick'],
        Backgrounds: []
      }

    }
  },
  mounted () {
    const images = this.importAll(require.context('./../assets/images/backgrounds', false, /\.(png|jpe?g|svg)$/))
    for (const key of Object.entries(images)) {
      this.decorations.Backgrounds.push(key[0].replace('.png', ''))
    }
  },
  methods: {
    importAll (folder) {
      const images = {}
      folder.keys().map((item, index) => { images[item.replace('./', '')] = folder(item) })
      return images
    }
  }
}

</script>
<style scoped lang="scss">
@import '../assets/scss/main.scss';
.main__container{
  width: 100%;
  height: 80%;
  margin: auto auto;
  padding: 20px;
  h1{
    font-family: 'Acme', sans-serif;
    @include text-style(50px, 500, $dark-blue);
    margin-bottom: 20px;
  }
  .interaction{
    display: flex;
    &__left-content{
      margin-right: 20px;
      &__image-wrapper{
        width: 300px;
        height: 300px;
        position: relative;
        &__bg{
          img{
            width: 300px;
            height: 300px;
          }
        }
        &__body{
          &__items{
            position: absolute;
            top: 0;
            left: 0;
            img{
              width: 300px;
              height: 300px;
            }
          }
        }
      }
    }
    &__select-wrapper__category__title{
      @include text-style(16px, 600, $dark-blue);
      margin-bottom: 10px;
      margin-left: 10px;
    }

}
}

</style>
