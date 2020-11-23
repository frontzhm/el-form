<template lang="pug">
  div
    label(v-if="label") {{label}}
    slot
    span {{errorMessages}}
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
    return { errorMessages: "" };
  },
  methods: {
    validate() {
      const modelKey = this.prop;
      const value = this.elForm.model[modelKey];
      const rule = this.elForm.rules[modelKey];
      // 通过描述信息创建一个骨架
      const schema = new Schema({ [modelKey]: rule });
      // 异步操作封装成promsie,将结果扔出去
      return new Promise(resolve => {
        schema.validate({ [modelKey]: value }, err => {
          // 没有错误，就说明是有效值
          if (!err) {
            this.errorMessages = "";
            resolve({ isValid: true });
            return;
          }
          // 错误的话，拿到所有的错误信息列表
          let errorMessages = err.map(item => item.message);
          this.errorMessages = errorMessages[0];
          resolve({ isValid: false, errorMessages });
        });
      });
    }
  }
};
</script>
