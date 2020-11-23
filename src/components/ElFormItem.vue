<template lang="pug">
  div
    label(v-if="label") {{label}}
    slot
</template>
<script>
export default {
  name: "ElFormItem",
  props: {
    label: String,
    prop: String
  }
};
</script>
