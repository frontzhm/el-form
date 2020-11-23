<template lang="pug">
  div
    label(v-if="label") {{label}}
    slot
    span {{errorMessage}}
</template>
<script>
import Schema from "async-validator";
export default {
  name: "ElFormItem",
  inject: ["elForm"],
  props: {
    label: String,
    prop: String
  },
  data() {
    return { errorMessage: "" };
  },
  methods: {
    validate() {
      const modelKey = this.prop;
      // 这里 如果没有modelKey的话就不用往下了
      if (!modelKey) {
        return;
      }
      const value = this.elForm.model[modelKey];
      const rule = this.elForm.rules[modelKey];
      // 通过描述信息创建一个骨架
      const schema = new Schema({ [modelKey]: rule });
      // 验证，返回的是一个promise，其实就是async-validator的结果
      return schema.validate({ [modelKey]: value }, err => {
        this.errorMessage = err ? err[0].message : "";
      });
    }
  }
};
</script>
