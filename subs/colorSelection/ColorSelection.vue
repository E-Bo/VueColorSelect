<template>
  <div class="v-color-selection-container">
    <div class="v-color-selection-colors-row" v-for="(index, row) in selection">
      <color-item :name="name" v-for="(innerIndex, item) in row" :value="row[innerIndex]" :model.sync="model"></color-item>
    </div>
  </div>
</template>
<script>
import colorItem from '../colorSelectionItem/ColorSelectionItem'

export default {
  props: {
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
    model: {
      required: false,
      twoWay: true
    },
    name: {
      required: false,
      default: 'colorSelect'
    }
  },
  data () {
    return {
    }
  },
  components: {
    colorItem
  },
  compiled () {
  },
  ready () {
  },
  methods: {
  },
  watch: {
  }
}
</script>

<style src="./colorSelection.less" lang="less"></style>
