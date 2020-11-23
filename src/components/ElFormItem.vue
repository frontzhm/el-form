<template lang="pug">
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
  mounted() {
    console.log(this.elForm.rules);
  },
  validate() {}
};
</script>
