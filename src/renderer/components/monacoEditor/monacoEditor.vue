<template>
  <div class="editor-wrapper">
    <div :id="editorId" class="editor"></div>
  </div>
</template>

<script>
  import * as monaco from 'monaco-editor/esm/vs/editor/editor.api'
  export default {
    name: 'monacoEditor',
    props: {
      // options: {
      //   type: Object,
      //   default: {}
      // },
      width: {
        type: String,
        default: '100%'
      },
      height: {
        type: String,
        default: '100%'
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
        value: `function hello() {\n\talert('Hello world!');\n}`,
        language: 'javascript',
        automaticLayout: true
      })
      const vm = this
      editor.onKeyUp(function (e) {
        console.log(e)
        vm.$emit('onKeyUp', e.browserEvent)
      })
    }
  }
</script>

<style scoped lang="scss">
  .editor-wrapper{
    width: 100%;
    height: 100%;
  }
  .editor{
    /*width: 300px;*/
    /*height: 100px;*/
    width: 100%;
    height: 100%;
  }
</style>
