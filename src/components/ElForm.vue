<template lang="pug">
  div el-form
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
  methods: {
    validate() {
      console.log("el-form的validate");
    }
  }
};
</script>
