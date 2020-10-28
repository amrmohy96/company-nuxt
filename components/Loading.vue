<template>
  <div class="demo-spin-col">
    <Spin fix>
      <Icon type="ios-loading" size=35 class="demo-spin-icon-load"></Icon>
    </Spin>
  </div>
</template>

<script>
export default {
  name: "Loading"
}
</script>
<style>
.demo-spin-icon-load{
  animation: ani-demo-spin 1s linear infinite;
}
@keyframes ani-demo-spin {
  from { transform: rotate(0deg);}
  50%  { transform: rotate(180deg);}
  to   { transform: rotate(360deg);}
}
.demo-spin-col{
  height: 100px;
  position: relative;
}
</style>
