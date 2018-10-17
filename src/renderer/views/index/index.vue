<template>
  <div class="main">

    <Split v-model="split1" class="area-work-split">
      <div slot="left" class="area left"  @input="change">
        <monaco-editor @onKeyUp="change"></monaco-editor>
      </div>
      <div slot="right" class="area right" v-html="compiledMarkdown"></div>
    </Split>
  </div>
</template>

<script>
  import _ from 'lodash'
  import MarkdownIt from 'markdown-it'
  import monacoEditor from '@c/monacoEditor/monacoEditor'

  export default {
    components: {
      monacoEditor
    },
    data () {
      return {
        split1: 0.5,
        input: ''
      }
    },
    computed: {
      compiledMarkdown: function () {
        const md = MarkdownIt()
        return md.render(this.input)
      }
    },
    methods: {
      change: _.throttle(function (e) {
        console.log(e)
        this.input = e.target.innerText
      }, 500)
    },
    mounted () {
    }
  }
</script>

<style scoped lang="scss">
  .main {
    height: 100%;

    .area-work-split {
      border: solid 1px #ddd;

      .area {
        height: 100%;
        &.right {
          margin-left: 10px;
        }

        #editor{
          /*width: 300px;*/
          /*height: 100px;*/
          width: 100%;
          height: 100%;
        }
      }
    }
  }
</style>
