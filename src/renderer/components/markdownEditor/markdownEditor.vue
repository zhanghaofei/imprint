<template>
  <div class="markdown-editor">
    <div class="top-area">
      <Dropdown>
        <Button size="small" type="primary">
          标题<Icon type="ios-arrow-down"></Icon>
        </Button>
        <DropdownMenu slot="list">
          <DropdownItem><Tooltip content="# H1" theme="light" :delay="500"><H1>H1</H1></Tooltip></DropdownItem>
          <DropdownItem><Tooltip content="## H1" theme="light" :delay="500"><H2>H2</H2></Tooltip></DropdownItem>
          <DropdownItem><Tooltip content="标题" theme="light" :delay="500"><H3>H3</H3></Tooltip></DropdownItem>
          <DropdownItem><Tooltip content="标题" theme="light" :delay="500"><H4>H4</H4></Tooltip></DropdownItem>
          <DropdownItem><Tooltip content="标题" theme="light" :delay="500"><H5>H5</H5></Tooltip></DropdownItem>
          <DropdownItem><Tooltip content="标题" theme="light" :delay="500"><H6>H6</H6></Tooltip></DropdownItem>
        </DropdownMenu>
      </Dropdown>
      <Divider type="vertical" />
      <ButtonGroup>
        <Button size="small" type="primary"><Tooltip content="标题" theme="light" :delay="500">B</Tooltip></Button>
        <Button size="small" type="primary"><Tooltip content="标题" theme="light" :delay="500">I</Tooltip></Button>
        <Button size="small" type="primary"><Tooltip content="标题" theme="light" :delay="500">S</Tooltip></Button>
      </ButtonGroup>
      <ButtonGroup>
        <Button size="small" type="primary">
          <Poptip>
            啊啊
            <div slot="content">

              <Button type="primary">插入</Button>
            </div>
          </Poptip>
        </Button>
      </ButtonGroup>
    </div>
    <div class="middle-area">
      <baseMonacoEditor
        ref="editor"
        v-model="myValue"
        @onDidChangeModelContent="onDidChangeModelContent"
        @onMouseMove="onMouseMove"
      ></baseMonacoEditor>
      <baseMonacoEditor> </baseMonacoEditor>
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
      }, 1000)
    },
    created () {
      // console.log(this.$refs)
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
      padding: 5px;
      border-bottom: solid 1px #e6e6e6;
    }
    .middle-area{
      flex: 1;
    }
    .bottom-area{
      flex: none;
      /*height: 40px;*/
      /*border: dashed 1px;*/

    }


  }
</style>
