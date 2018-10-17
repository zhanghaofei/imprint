<template>
  <div class="markdown-editor">
    <div class="top-area"></div>
    <div class="middle-area">
      <baseMonacoEditor v-model="myValue" @onDidChangeModelContent="onDidChangeModelContent"></baseMonacoEditor>
    </div>
    <div class="bottom-area" v-html="myValue"></div>

  </div>
</template>

<script>
  import _ from 'lodash'
  import baseMonacoEditor from '@c/baseMonacoEditor/baseMonacoEditor'
  export default {
    name: 'markdownEditor',
    components: { baseMonacoEditor },
    props: {
      value: {
        type: String,
        default: `# H1\n## H2\n内容`
      }
    },
    data () {
      return {
        myValue: this.value
      }
    },
    methods: {
      onDidChangeModelContent: _.throttle(function (e) {
        console.log(e)
        this.$emit('input', this.myValue)
      }, 500)
    },
    created () {
    }
  }
</script>

<style scoped lang="scss">
  .markdown-editor{
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;

    .top-area{
      flex: none;
      height: 50px;
      border: dashed 1px;
    }
    .middle-area{
      flex: 1;
    }
    .bottom-area{
      flex: none;
      height: 50px;
      border: dashed 1px;

    }

  }
</style>
