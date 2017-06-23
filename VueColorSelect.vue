<template>
  <div class="v-color-select-container" :class="{ 'disabled': disabled, 'show-drop': showDrop }">
    <div class="v-color-select-colors-container">
      <color-item v-for="(index, item) in model" @click="handleDropdown(index)" :model.sync="selectedColorIndex" :value="index" :color="item" selected-style="underline" track-by="$index"></color-item>
    </div>
    <div class="v-color-select-selection-container" :class="{ 'drop-right': !dropLeft }" @click.stop="">
      <div class="v-color-select-selection-top">
        <div class="color-value-text">
          {{ currentColor }}
        </div>
        <div class="">
          <color-item v-show="tmpColor" :model.sync="currentColor" :name="selectionName" :value="tmpColor"></color-item>
        </div>
      </div>
      <color-selection :name="selectionName" :selection="selection" :model.sync="currentColor"></color-selection>
    </div>
  </div>
</template>
<script>
import colorItem from './subs/colorSelectionItem/ColorSelectionItem'
import colorSelection from './subs/colorSelection/ColorSelection'

export default {
  props: {
    name: {
      required: false,
      type: String,
      default: 'vueColorSelect'
    },
    model: {
      required: false,
      type: Array,
      twoWay: true
    },
    selection: {
      required: false,
      type: Array,
      default () {
        return [
          ['#ffcdd2', '#ef9a9a', '#e57373', '#ef5350', '#f44336', '#e53935', '#d32f2f', '#c62828', '#b71c1c'],
          ['#ffe0b2', '#ffcc80', '#ffb74d', '#ffa726', '#ff9800', '#fb8c00', '#f57c00', '#ef6c00', '#e65100'],
          ['#fff9c4', '#fff59d', '#fff176', '#ffee58', '#ffeb3b', '#fdd835', '#fbc02d', '#f9a825', '#f57f17'],
          ['#c8e6c9', '#a5d6a7', '#aed581', '#66bb6a', '#4caf50', '#43a047', '#388e3c', '#2e7d32', '#1b5e20'],
          ['#bbdefb', '#90caf9', '#64b5f6', '#42a5f5', '#2196f3', '#1e88e5', '#1976d2', '#1565c0', '#0d47a1']
        ]
      }
    },
    dropLeft: {
      required: false,
      type: Boolean,
      default: false
    },
    disabled: {
      required: false,
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      selectionName: 'colorSelect',
      selectedColorIndex: -1,
      showDrop: false,
      testTimer: null,
      tmpColor: '',
      openState: false,
      markNum: 0
    }
  },
  computed: {
    currentColor: {
      set (newValue) {
        if (this.selectedColorIndex !== -1 && this.selectedColorIndex < this.model.length) {
          this.model.$set(this.selectedColorIndex, newValue)
        }
      },
      get () {
        if (this.selectedColorIndex !== -1) {
          return this.model[this.selectedColorIndex]
        } else {
          return ''
        }
      }
    }
  },
  components: {
    colorItem,
    colorSelection
  },
  compiled () {
  },
  ready () {
    this.addDocEvent()
  },
  destroyed () {
    this.clearDocEvent()
  },
  methods: {
    hideDropdown () {
      this.selectedColorIndex = -1
      this.showDrop = false
    },
    showDropdown () {
      this.showDrop = true
      this.openState = true
    },
    docCallback () {
      if (!this.openState) {
        this.hideDropdown()
      }
      this.openState = false
    },
    handleDropdown (index, e) {
      e = e || window.event
      let element = e.target || e.srcElement
      if (element.tagName !== 'INPUT') {
        // 禁用掉非 input 的那次事件，因为 input 触发的那次事件
        // 会默认修改一次自身绑定的 v-model(即 this.selectedColorIndex)，
        // 而且会发生在非 input 事件之后，
        // 也就是说如果之前先修改 v-model 绑定的值，当 input 的事件再次触发时，
        // 又会将 v-model 绑定的值修改为此 input 的 value 值，之后再执行回调，而这个结果不是我们想要的

        // 同时关闭非 INPUT 触发事件的事件冒泡
        if (e.stopPropagation) {
          e.stopPropagation()
        } else {
          e.cancelBubble = true
        }
        return false
      } else {
        if (index === this.selectedColorIndex && this.showDrop) {
          this.hideDropdown()
        } else {
          this.showDropdown()
        }
      }
    },
    addDocEvent () {
      document.addEventListener('click', this.docCallback)
    },
    clearDocEvent () {
      document.removeEventListener('click', this.docCallback)
    }
  },
  watch: {
    selectedColorIndex (val, oldVal) {
      this.tmpColor = this.currentColor
    }
  }
}
</script>

<style src="./vueColorSelect.less" lang="less"></style>
