<!-- 小卡片 -->
<template>
  <div class="card">
    <div class="card-item">
      {{ name }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: { type: String, default: "" }
  }
}
</script>

<style scoped lang="scss">
.card {
  font-size: 16px;
  padding: 0.1rem 0rem 0.1rem 0.1rem;
  box-shadow: 0rem 0rem 10px #0a43bc;
  .card-item {
    border-left: 0.05rem solid #1890ff;
    padding-left: 0.1rem;
  }
}
</style>
