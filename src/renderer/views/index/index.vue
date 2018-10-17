<template>
  <div class="main">

    <Split v-model="split1" class="area-work-split">
      <div slot="left" class="area left">
        <markdown-editor v-model="markdown"></markdown-editor>
      </div>
      <div slot="right" class="area right" v-html="compiledMarkdown"></div>
    </Split>
  </div>
</template>

<script>
  import MarkdownIt from 'markdown-it'
  import markdownEditor from '@c/markdownEditor/markdownEditor'

  export default {
    components: {
      markdownEditor
    },
    data () {
      return {
        split1: 0.5,
        markdown: `function hello() {\n\talert('Hello world!');\n}`
      }
    },
    computed: {
      compiledMarkdown: function () {
        const md = MarkdownIt()
        return md.render(this.markdown)
      }
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
