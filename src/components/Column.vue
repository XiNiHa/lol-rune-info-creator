<template>
  <div class="rune-column">
    <div class="expander"/>
    <div class="rune-row">
      <img :src="assetURLs.빌드[build]" class="rune-build">
    </div>
    <div v-if="isMain" class="rune-row rune-row-keystone">
      <div v-for="(rune, key, i) in assetURLs[build].키스톤" :key="i"  :class="{'rune-item-active': selected[0] === i, 'rune-item': true}" @click="toggleRune(0, i)">
        <img :src="rune">
        <span class="rune-tooltip">{{ key.replace(/_/g, ' ') }}</span>
      </div>
    </div>
    <div v-for="(row, i) in assetURLs[build].서브룬" :key="i" class="rune-row">
      <div v-for="(rune, key, j) in row" :key="j" :class="{'rune-item-active': selected[i + 1] === j, 'rune-item': true}" @click="toggleRune(i + 1, j)">
        <img :src="rune">
        <span class="rune-tooltip">{{ key.replace(/_/g, ' ') }}</span>
      </div>
    </div>
    <div class="expander"/>
  </div>
</template>

<script>
import assetURLs from '../assetURLs'

export default {
  props: {
    isMain: {
      type: Boolean,
      default: false
    },
    build: {
      type: String,
      default: '정밀'
    }
  },
  data () {
    return {
      assetURLs,
      selected: [-1, -1, -1, -1],
      selectCount: 0
    }
  },
  methods: {
    toggleRune (row, col) {
      this.$emit('change')
      if (this.selected[row] === col) {
        return this.$set(this.selected, row, -1)
      }

      let row1 = -1
      let row2 = -1
      if (!this.isMain) {
        switch (row) {
          case 1:
            row1 = 2
            row2 = 3
            break
          case 2:
            row1 = 1
            row2 = 3
            break
          case 3:
            row1 = 1
            row2 = 2
            break
        }
      }

      if (this.selected[row1] !== -1 && this.selected[row2] !== -1) {
        this.$set(this.selected, row1, -1)
        this.$set(this.selected, row2, -1)
      }

      this.$set(this.selected, row, col)
    }
  }
}
</script>
