<template>
  <div class="rune-generator">
    <div class="rune-selection">
      <select v-model="mainBuild">
        <option value="정밀">정밀</option>
        <option value="지배">지배</option>
        <option value="마법">마법</option>
        <option value="결의">결의</option>
        <option value="영감">영감</option>
      </select>
      <select v-model="subBuild">
        <option value="정밀">정밀</option>
        <option value="지배">지배</option>
        <option value="마법">마법</option>
        <option value="결의">결의</option>
        <option value="영감">영감</option>
      </select>
    </div>
    <div id="rune-columns-wrapper">
      <div class="rune-columns">
        <app-column :is-main="true" :build="mainBuild" @change="$emit('change')"/>
        <app-column :build="subBuild" @change="$emit('change')"/>
      </div>
    </div>
  </div>
</template>

<script>
import appColumn from './Column.vue'

export default {
  components: {
    appColumn
  },
  data () {
    return {
      mainBuild: undefined,
      subBuild: undefined
    }
  }
}
</script>
