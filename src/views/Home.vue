<template>
  <div class="main__container">
    <h1>ALPACA GENERATOR</h1>
    <div class="interaction">
      <div class="interaction__left-content">
        <div class="interaction__left-content__image-wrapper download-img">
          <div class="interaction__left-content__image-wrapper__bg">
            <img
              :src="require(`./../assets/images/backgrounds/${ alpacaStyle.Backgrounds? alpacaStyle.Backgrounds : 'blue50'}.png`)"
              alt="backgrounds"
            >
          </div>
          <div class="interaction__left-content__image-wrapper__body">
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                :src="require(`./../assets/images/ears/${ alpacaStyle.Ears? alpacaStyle.Ears : 'default'}.png`)"
                alt="ears"
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                :src="require(`./../assets/images/hair/${ alpacaStyle.Hair ? alpacaStyle.Hair : 'default'}.png`)"
                alt="Hair"
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                :src="require(`./../assets/images/leg/${ alpacaStyle.Leg ? alpacaStyle.Leg : 'default'}.png`)"
                alt="leg"
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                :src="require(`./../assets/images/neck/${ alpacaStyle.Neck ? alpacaStyle.Neck : 'default'}.png`)"
                alt="neck"
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
                :src="require(`./../assets/images/eyes/${ alpacaStyle.Eyes ? alpacaStyle.Eyes : 'default'}.png`)"
                alt="eyes"
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <img
                :src="require(`./../assets/images/mouth/${ alpacaStyle.Mouth ? alpacaStyle.Mouth : 'default'}.png`)"
                alt="mouth"
              >
            </div>
            <div class="interaction__left-content__image-wrapper__body__items">
              <template v-if="alpacaStyle.Accessories && alpacaStyle.Accessories !=='default'">
                <img
                  :src="require(`./../assets/images/accessories/${ alpacaStyle.Accessories}.png`)"
                  alt="Accessories"
                >
              </template>
            </div>
          </div>
          <div class="interaction__left-content__image-wrapper__decoration" />
        </div>
        <div class="interaction__left-content__btn-wrapper">
          <FunctionalBtns
            @random-style="randomStyle"
            @reset="reset"
            @downloadImg="downloadImg"
          />
        </div>
      </div>
      <div class="interaction__select-wrapper">
        <div class="interaction__select-wrapper__category">
          <div class="interaction__select-wrapper__category__title">
            ACCESSORIZE THE ALPACA'S
          </div>
          <div class="interaction__select-wrapper__category__item">
            <Selection
              v-for="category in categories"
              :key="categories.indexOf(category)"
              :category="category"
              :checked="selectedCategory===category"
              @after-selected="handleSelected"
            />
          </div>
        </div>
        <div
          v-if="isSelected"
          class="interaction__select-wrapper__category--selected"
        >
          <div class="interaction__select-wrapper__category__title">
            STYLE
          </div>
          <div class="interaction__select-wrapper__category__item">
            <Selection
              v-for="item in selected"
              :key="selected.indexOf(item)"
              :category="item"
              :checked="alpacaStyle[selectedCategory] === item"
              @after-selected="handleSelectedItem"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Selection from './../components/Selection.vue'
import html2canvas from 'html2canvas'
import FunctionalBtns from './../components/FunctionalBtns.vue'

export default {
  name: 'Home',
  components: {
    Selection,
    FunctionalBtns
  },
  data () {
    return {
      categories: ['Hair', 'Ears', 'Eyes', 'Leg', 'Mouth', 'Neck', 'Accessories', 'Backgrounds'],
      decorations: {
        Hair: ['default', 'bang', 'curls', 'elegant', 'fancy', 'quiff', 'short'],
        Ears: ['default', 'tilt-backward', 'tilt-forward'],
        Eyes: ['default', 'angry', 'naughty', 'panda', 'smart', 'star'],
        Leg: ['default', 'bubble-tea', 'cookie', 'game-console', 'tilt-backward', 'tilt-forward'],
        Mouth: ['default', 'astonished', 'eating', 'laugh', 'tongue'],
        Neck: ['default', 'bend-backward', 'bend-forward', 'thick'],
        Accessories: ['default', 'earings', 'flower', 'glasses', 'headphone'],
        Backgrounds: []
      },
      selected: [],
      isSelected: false, // 控制style區塊是否出現
      selectedCategory: '',
      selectedItem: '',
      alpacaStyle: {
        Hair: '',
        Ears: '',
        Eyes: '',
        Leg: '',
        Mouth: '',
        Neck: '',
        Accessories: '',
        Backgrounds: ''
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
    async downloadImg () {
      const images = document.querySelector('.download-img')
      const canvas = await html2canvas(images)
      const imgData = canvas.toDataURL('image/jpeg')
      // set the name of the download file
      const downloadLink = document.createElement('a')
      downloadLink.download = 'cuteAlpaca.jpeg'
      downloadLink.href = imgData
      document.body.appendChild(downloadLink)
      downloadLink.click()
      document.body.removeChild(downloadLink)
    },
    importAll (folder) {
      const images = {}
      folder.keys().map((item) => { images[item.replace('./', '')] = folder(item) })
      return images
    },
    handleSelected (category) {
      this.selectedCategory = ''
      this.selectedItem = ''
      this.isSelected = true
      this.selected = [...this.decorations[category]]
      this.selectedCategory = category
    },
    handleSelectedItem (item) {
      const category = this.selectedCategory
      this.alpacaStyle[category] = item
      this.selectedItem = item
    },
    randomStyle () {
      for (const item in this.decorations) {
        const index = Math.floor(Math.random() * this.decorations[item].length)
        this.alpacaStyle[item] = this.decorations[item][index]
      }
    },
    reset () {
      for (const item in this.alpacaStyle) {
        this.alpacaStyle[item] = ''
      }
    }
  }
}

</script>
<style scoped lang="scss">
@import '../assets/scss/main.scss';
.main__container{
  width: 95%;
  margin: 0 auto;
}
  h1{
    @include text-style(30px, 500, $dark-blue);
    width: 95%;
    margin: 20px auto;
  }
  .interaction{
    width: 95%;
    margin: auto;
    display: flex;
    flex-direction: column;
    &__left-content{
      margin: 0 auto 16px auto;
      &__image-wrapper{
        width: 90%;
        margin:0 auto;
        height: auto;
        position: relative;
        &__bg{
          img{
            width: 100%;
            height: 100%;
          }
        }
        &__body{
          &__items{
            position: absolute;
            top: 0;
            left: 0;
            img{
              width: 100%;
              height: 100%;
            }
          }
        }
      }
      &__btn-wrapper{
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 8px;
        width: 100%;
        margin: 8px 0;
      }
    }
    &__select-wrapper{
      width: 100%;
      margin: 0 auto;
      &__category{

        position: relative;
        &__item{
          display: flex;
          max-height: 100px;
          overflow-x: scroll;
          white-space: nowrap

        }
        &--selected{
          margin-top: 16px;
          height: 45%;

        }
        &__title{
          @include text-style(16px, 600, $dark-blue);
          margin-bottom: 10px;
          margin-left: 10px;
        }
      }
    }
}
@media screen and (min-width: 480px) {

  h1{
    @include text-style(30px, 500, $dark-blue);
    width: 95%;
  }
  .interaction{
    flex-direction: row;
    &__left-content{
      margin-right: 20px;
      width: 90%;
      &__image-wrapper{
        margin: 0;
        width: 100%;
      }
      &__btn-wrapper{
        display: grid;
        width: 100%;
        grid-template-rows: 1fr 1fr ;
        grid-template-columns: 1fr 1fr;
        grid-column-gap: 16px;
        margin-top: 16px;

      }
    }
    &__select-wrapper__category{
      &__item{
        display: flex;
        flex-wrap: wrap;
        max-height: 150px;
        overflow-y: scroll;

      }
      &--selected{
        margin-top: 16px;
        height: 45%;

      }
      &__title{
        @include text-style(16px, 600, $dark-blue);
        margin-bottom: 10px;
        margin-left: 10px;
      }
    }

}
}
@media screen and (min-width: 768px) {
  .main__container{
    width: 90%;
  }
  h1{
    @include text-style(50px, 500, $dark-blue);

  }
  .interaction{
    width: 95%;
    &__left-content{
      width: auto;
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
      &__btn-wrapper{
        display: grid;
        width: 300px;
        grid-template-rows: 1fr 1fr ;
        grid-template-columns: 1fr 1fr;
        grid-column-gap: 16px;
        margin-top: 16px;
      }
    }
    &__select-wrapper__category{

      &__item{
        display: flex;
        flex-wrap: wrap;
        max-height: 170px;
        overflow-y: scroll;

      }
      &--selected{
        margin-top: 16px;
        height: 45%;

      }
      &__title{
        font-size: 20px;
      }
    }

}
}
</style>
