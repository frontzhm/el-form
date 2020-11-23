<template lang="pug">
  input(:value="value" @input="handleInput")
</template>

<script>
export default {
  name: "ElInput",
  props: {
    value: String
  },
  methods: {
    handleInput(e) {
      this.$emit("input", e.target.value);
      this.triggerValidate();
    },
    triggerValidate() {
      let parent = this.$parent;
      while (parent) {
        const isElFormItem = parent.$options.name === "ElFormItem";
        if (isElFormItem) {
          parent.validate();
          break;
        }
        parent = parent.$parent;
      }
    }
  }
};
</script>
