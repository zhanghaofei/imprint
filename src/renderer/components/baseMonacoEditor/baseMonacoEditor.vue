<template>
  <div :id="editorId" class="editor"></div>
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
      const editor = monaco.editor.create(document.getElementById(this.editorId), {
        value: this.value,
        language: 'javascript',
        automaticLayout: true
      })
      const vm = this
      editor.onDidChangeModelContent(function (e) {
        vm.$emit('onDidChangeModelContent', e)
        vm.$emit('input', editor.getValue())
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
