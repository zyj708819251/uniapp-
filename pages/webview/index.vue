<template>
  <web-view :src="wlurl"></web-view>
</template>

<script>
export default {
  data() {
    return {
      wlurl: 'http://www.baidu.com'
    }
  },
  onLoad(item) {
    // this.url = decodeURIComponent(item.url)
    // console.log(this.url)
    // 传入需要跳转的链接 使用web-view标签进行跳转
  }
}
</script>

<style lang="scss">
</style>


