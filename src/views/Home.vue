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
          </div>
          <div class="interaction__left-content__image-wrapper__decoration" />
        </div>
        <div class="interaction__left-content__btn-wrapper">
          <button
            class="functional-btn"
            @click.stop.prevent="randomStyle"
          >
            <img
              src="./../assets/icons/dices.svg"
              alt=""
            >
            Random
          </button>
          <button
            class="functional-btn"
            @click.stop.prevent="downloadImg"
          >
            <img
              src="./../assets/icons/download.svg"
              alt=""
            >Download
          </button>
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
              :checked="selectedItem === item"
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

export default {
  name: 'Home',
  components: {
    Selection
  },
  data () {
    return {
      categories: ['Hair', 'Ears', 'Eyes', 'Leg', 'Mouth', 'Neck', 'Backgrounds'],
      decorations: {
        Hair: ['bang', 'curls', 'elegant', 'fancy', 'quiff', 'short'],
        Ears: ['tilt-backward', 'tilt-forward'],
        Eyes: ['angry', 'naughty', 'panda', 'smart', 'star'],
        Leg: ['bubble-tea', 'cookie', 'game-console', 'tilt-backward', 'tilt-forward'],
        Mouth: ['astonished', 'eating', 'laugh', 'tongue'],
        Neck: ['bend-backward', 'bend-forward', 'thick'],
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
      const imgData = canvas.toDataURL('image/jpeg');

      (function (imgData) {
        const downloadLink = document.createElement('a')
        downloadLink.download = 'cuteAlpaca.jpeg' // set the name of the download file
        downloadLink.href = imgData
        document.body.appendChild(downloadLink)
        downloadLink.click()
        document.body.removeChild(downloadLink)
      })(imgData)
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
    }
  }
}

</script>
<style scoped lang="scss">
@import '../assets/scss/main.scss';
.main__container{
  width: 80%;
  height: 80%;
  margin: auto auto;
  padding: 20px;
}
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
      &__btn-wrapper{
        display: grid;
        width: 300px;
        grid-template-columns: 1fr 1fr;
        grid-column-gap: 16px;
        margin-top: 16px;
         .functional-btn{
          background: #fff;
          height: 40px;
          width: 100%;
          line-height: 40px;
          margin-right: 16px;
          display: flex;
          justify-content: center;
          &:hover{
            box-shadow: 1px 1px 5px 0px rgba(143,140,140,0.75);
            transition: box-shadow 0.2s ease-in;
          }
          img{
            margin: auto 10px auto 0;
            width: 20px;
            height: 20px;
          }
        }
      }
    }
    &__select-wrapper__category{
      &--selected{
        margin-top: 10px;
      }
      &__title{
        @include text-style(16px, 600, $dark-blue);
        margin-bottom: 10px;
        margin-left: 10px;
      }
    }

}
</style>
