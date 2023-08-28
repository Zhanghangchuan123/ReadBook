<template>
  <div id="app">
    <router-view/>
  </div>
</template>
<script>
export default {}
document.addEventListener('DOMContentLoaded', () => {
  const html = document.querySelector('html')
  let fontSize = window.innerWidth / 10
  // 给fontSize设置一个上限，防止过大
  fontSize = fontSize > 50 ? 50 : fontSize
  html.style.fontSize = fontSize + 'px'
})
</script>
<style scoped>
#app {
  width: 100%;
  height: 100%;
  overflow: hidden;
}
</style>
