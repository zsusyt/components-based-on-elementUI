<!--suppress ALL -->
<template>
    <div class="container">
      <div class="element preLabel" v-if="preLabel !== undefined">
        <span>{{preLabel}}</span>
      </div><div class="element" v-if="$slots.preInput" :class="preInputClass">
        <slot name="preInput"></slot>
      </div><el-select v-model="selectModel" :class="selectClass">
        <el-option value="1">1</el-option>
        <el-option value="2">2</el-option>
        <el-option value="3">3</el-option>
      </el-select><div class="element" v-if="$slots.appInput" :class="appInputClass">
        <slot name="appInput"></slot>
      </div><div class="element appLabel" v-if="appLabel !== undefined">
        <span>{{appLabel}}</span>
      </div>
    </div>
</template>

<script>
  export default {
    name: "ispSelect",
    props: {
      selectModel: {
        type: String,
        required: true
      },
      preLabel: String,
      appLabel: String
    },
    computed: {
      selectClass () {
        if (this.preLabel !== undefined || this.$slots.preInput) {
          if(this.appLabel !== undefined || this.$slots.appInput) {
            return "select-with-all"
          } else {
            return "select-with-left"
          }
        } else {
          if(this.appLabel !== undefined || this.$slots.appInput) {
            return "select-with-right"
          } else {
            return ""
          }
        }
      },
      preInputClass () {
        if (this.preLabel === undefined) {
          return "preInput-without-left"
        } else {
          return "preInput-with-all"
        }
      },
      appInputClass () {
        if (this.appLabel === undefined) {
          return "appInput-without-right"
        } else {
          return "appInput-with-all"
        }
      }
    }
  }
</script>

<style scoped lang="scss">

.container {
  .element {
    display: inline-block;
    /*border: 1px solid;*/
    line-height: 38px;
    box-sizing: border-box;
  }
  .preLabel {
    padding: 0 10px;
    border: 1px solid #DCDFE6;
    border-right: none;
    border-radius: 10px 0 0 10px;
  }
  .appLabel {
    padding:0 10px;
    border: 1px solid #DCDFE6;
    border-left: none;
    border-radius: 0 10px 10px 0;
  }
}
</style>

<style lang="scss">
  .preInput-with-all,
  .preInput-without-left{
    .el-input__inner {
      border-right: 0;
    }
  }

  .appInput-with-all,
  .appInput-without-right{
    .el-input__inner {
      border-left: 0;
    }
  }

  .select-with-all,
  .preInput-with-all,
  .appInput-with-all {
    .el-input__inner {
      border-radius: 0;
    }
  }

  .select-with-left,
  .appInput-without-right{
    .el-input__inner {
      border-radius: 0 10px 10px 0;
    }
  }

  .select-with-right,
  .preInput-without-left{
    .el-input__inner {
      border-radius: 10px 0 0 10px;
    }
  }

</style>
