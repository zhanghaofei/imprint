<template>
  <div class="markdown-editor">
    <div class="top-area"></div>
    <div class="middle-area">
      <baseMonacoEditor
        v-model="myValue"
        @onDidChangeModelContent="onDidChangeModelContent"
        @onMouseMove="onMouseMove"
      ></baseMonacoEditor>
    </div>
    <div class="bottom-area"></div>

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
        default: ''
      }
    },
    data () {
      return {
        myValue: this.value
      }
    },
    methods: {
      onDidChangeModelContent: _.debounce(function (e) {
        this.$emit('input', this.myValue)
      }, 100),
      onMouseMove: _.debounce(function (e) {
        console.log(e)
        console.log(e.target.element.innerText)
      }, 1000)
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
