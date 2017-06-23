<template>
  <label class="v-color-selection-item-container" :class="{ 'disabled': disabled }" :style="{ 'width': width }">
    <input class="hidden-input v-color-selection-item-input" type="radio" :name="name" :value="value" v-model="model">
    <div class="v-color-selection-item-handler" :class="selectedStyle" :style="{ 'background-color': itemColor }">
    </div>
  </label>
</template>
<script>
export default {
  props: {
    name: {
      required: false,
      type: String,
      default: 'colorItem'
    },
    value: {
      required: true
    },
    color: {
      required: false,
      type: String,
      default: ''
    },
    model: {
      required: false,
      twoWay: true
    },
    width: {
      required: false,
      type: String,
      default: '1em'
    },
    disabled: {
      required: false,
      type: Boolean,
      default: false
    },
    selectedStyle: {
      required: false,
      type: String,
      default: 'default'
    }
  },
  data () {
    return {
    }
  },
  compiled () {
  },
  ready () {
  },
  components: {
  },
  computed: {
    itemColor () {
      return this.color || this.value
    }
  },
  methods: {
  },
  watch: {
  }
}
</script>

<style src="./colorSelectionItem.less" lang="less"></style>
