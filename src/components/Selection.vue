<template>
  <button
    class="circle-btn"
    :class="{checked:checked}"
    @click="selectItem"
  >
    {{ category }}
  </button>
</template>
<script>
export default {
  name: 'Selection',
  props: {
    category: {
      type: String,
      required: true
    },
    checked: {
      type: Boolean,
      default: false
    }
  },
  emits: {
    'after-selected': null
  },
  methods: {
    selectItem () {
      this.$emit('after-selected', this.category)
    }
  }

}
</script>
<style scoped lang="scss">
@import '../assets/scss/main.scss';

</style>
