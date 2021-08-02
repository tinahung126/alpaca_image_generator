<template>
  <button
    class="circle-btn"
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
