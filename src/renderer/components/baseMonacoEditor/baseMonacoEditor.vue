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
            automaticLayout: true,
            lineNumbersMinChars: 1
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
    methods: {
    },
    mounted () {
      this.options.value = this.value
      this.editor = monaco.editor.create(document.getElementById(this.editorId), this.options)
      const vm = this
      this.editor.onDidChangeModelContent(function (e) {
        vm.$emit('onDidChangeModelContent', e)
        vm.$emit('input', this.editor.getValue())
      })
      this.editor.onMouseMove(function (e) {
        vm.$emit('onMouseMove', e)
      })
      //
      this.getSelections = this.editor.getSelections
    }
  }
</script>

<style scoped lang="scss">
  .editor{
  }


  .monaco-editor .margin {
    background-color: #f3f3f3;
  }
</style>
