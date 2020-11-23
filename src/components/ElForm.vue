<template lang="pug">
  div
    div rules:{{rules}}
    div model:{{model}}
    slot
</template>
<script>
export default {
  name: "ElForm",
  props: {
    model: Object,
    rules: Object
  },
  provide() {
    return { elForm: this };
  },
  methods: {
    validate() {
      console.log("el-form的validate");
    }
  }
};
</script>
