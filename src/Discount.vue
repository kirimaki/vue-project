<template>
  <div class="discount">
    <h4>지금 결제하면 <span id="">{{ value }}</span>% 할인</h4>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Discount",
  props: {
    value : Number,
  },
  data() {
  },
  mounted() {
    this.$emit("transData", 25);
  }
}
</script>

<style scoped>
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>