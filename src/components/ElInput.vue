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
    }
  }
};
</script>
