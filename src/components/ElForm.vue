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
    async validate(fn) {
      const elFormItems = this.getElFormItems();
      const promises = elFormItems.map(item => item.validate());
      try {
        // 都返回正确的话，才会true
        await Promise.all(promises);
        fn(true);
      } catch (error) {
        fn(false);
      }
    },
    getElFormItems() {
      let elFormItems = [];
      let children = this.$children;
      const findElFormItems = children => {
        children.forEach(child => {
          const isElFormItem = child.$options.name === "ElFormItem";
          isElFormItem && elFormItems.push(child);
          // 递归的终止条件
          child.$children.length && findElFormItems(child.$children);
        });
      };
      findElFormItems(children);
      return elFormItems;
    }
  }
};
</script>
