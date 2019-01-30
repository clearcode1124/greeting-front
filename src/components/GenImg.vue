<template>
  <div class="gen-img">
      <img :src="this.$route.params.src" style="width:100%;height:100%;">
  </div>
</template>

<style>
.gen-image {
  width: 100%;
  height: 100%;
  margin-top: 10px;
  margin-bottom: 10px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  overflow: hidden;
}
</style>

