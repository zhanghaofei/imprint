<template>
  <div :id="editorId" class="editor" :style="{ width, height }"></div>
</template>

<script>
  import * as monaco from 'monaco-editor/esm/vs/editor/editor.api'
  export default {
    name: 'baseMonacoEditor',
    props: {
      width: {
        type: String,
        default: '100%'
      },
      height: {
        type: String,
        default: '100%'
      },
      value: {
        type: String,
        default: ''
      },
      options: {
        type: Object,
        default () {
          return {
            language: 'markdown',
            automaticLayout: true
          }
        }
      }
    },
    data () {
      return {
      }
    },
    computed: {
      editorId () {
        return `editor${this._uid}`
      }
    },
    mounted () {
      this.options.value = this.value
      const editor = monaco.editor.create(document.getElementById(this.editorId), this.options)
      const vm = this
      editor.onDidChangeModelContent(function (e) {
        vm.$emit('onDidChangeModelContent', e)
        vm.$emit('input', editor.getValue())
      })
      editor.onMouseMove(function (e) {
        vm.$emit('onMouseMove', e)
      })
    }
  }
</script>

<style scoped lang="scss">
  .editor{
    /*width: 300px;*/
    /*height: 100px;*/
    width: 100%;
    height: 100%;
  }
</style>
