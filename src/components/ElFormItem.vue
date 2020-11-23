<template lang="pug">
  div(v-if="label")
    hr
    div rule是{{elForm.rules[prop]}}
    div value是{{elForm.model[prop]}}
    div
      label(v-if="label") {{label}}
      slot
</template>
<script>
export default {
  name: "ElFormItem",
  inject: ["elForm"],
  props: {
    label: String,
    prop: String
  },
  methods: {
    validate() {
      console.log("ElFormItem的validate");
    }
  }
};
</script>
