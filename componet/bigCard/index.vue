<!-- 大卡片 -->
<template>
  <div
    class="card"
    :style="{ background: `linear-gradient(91deg, ${color1} 0%, ${color2} 100%)` }"
  >
    <p class="num">{{ num }}元</p>
    <p class="name">{{ name }}</p>
  </div>
</template>

<script>
/*  eslint-disable */

export default {
  props: {
    name: { type: String, default: "" },
    num: { type: Number, default: 0 },
    color1: { type: String, default: "" },
    color2: { type: String, default: "" }
  },
}
</script>

<style scoped lang="scss">
.card {
  padding: 0.1rem 0rem 0.1rem 0.1rem;
  text-align: center;
  border-radius: 0.1rem;
  .num {
    font-size: 0.36rem;
    padding: 0.1rem 0;
    margin: 0;
  }
  .name {
    font-size: 0.26rem;
    padding: 0.1rem 0;
    margin: 0;
  }
}
</style>
