<template>
  <div id="app">
    <app-rune-generator @change="processOutput"/>
    <textarea id="output"/>
  </div>
</template>

<script>
import appRuneGenerator from './components/RuneGenerator.vue'

export default {
  name: 'App',
  components: {
    appRuneGenerator
  },
  methods: {
    processOutput () {
      setTimeout(() => {
        let wrapperObject = document.getElementById('rune-columns-wrapper')
        document.getElementById('output').value = wrapperObject.innerHTML.replace(/ data-v-[^\s]+=""/g, '')
      }, 10)
    }
  }
}
</script>

<style>
/* only for app */
#app {
  display: flex;
}

#output {
  flex-grow: 1;
}

.rune-generator {
  width: 800px;
}

.rune-selection {
  display: flex;
  justify-content: space-around
}

select {
  width: 100px;
}

/* common */

.rune-columns {
  display: flex;
}

.rune-column {
  width: 400px;
  height: 500px;
  display: flex;
  flex-direction: column;
  border: 1px solid #ddd;
  background: #ebe9e9;
}

.expander {
  flex-grow: 1;
}

.rune-row {
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding-top: 10px;
}

.rune-build {
  width: 125px;
  height: 125px;
  border-radius: 50%;
}

.rune-item {
  position: relative;
  display: inline-block;
}

.rune-item img{
  width: 65px;
  height: 65px;
  opacity: 0.3;
  transition: opacity 0.2s;
}

.rune-row-keystone .rune-item img {
  width: 100px;
  height: 100px;
}

.rune-item-active img{
  opacity: 1.0;
}

.rune-item .rune-tooltip {
  visibility: hidden;
  width: 120px;
  background-color: #555;
  color: #fff;
  text-align: center;
  padding: 5px;
  border-radius: 8px;

  position: absolute;
  z-index: 1;
  bottom: 110%;
  left: 50%;
  margin-left: -60px;

  opacity: 0;
  transition: opacity 0.3s;
}

.rune-item .rune-tooltip::after {
    content: "";
    position: absolute;
    top: 100%;
    left: 50%;
    margin-left: -5px;
    border-width: 5px;
    border-style: solid;
    border-color: #555 transparent transparent transparent;
}

.rune-item:hover .rune-tooltip {
    visibility: visible;
    opacity: 1;
}
</style>
