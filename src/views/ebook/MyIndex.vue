<template>
  <div class="ebook">
    <ebook-title></ebook-title>
    <ebook-reader></ebook-reader>
    <ebook-menu></ebook-menu>
  </div>
</template>

<script>
import EbookTitle from '@/components/ebook/EbookTitle.vue'
import EbookMenu from '@/components/ebook/EbookMenu.vue'
import EbookReader from '@/components/ebook/EbookReader.vue'
import { getReadTime, saveReadTime } from '@/utils/localStorage'
import { ebookMixin } from '@/utils/mixin'
export default {
  mixins: [ebookMixin],
  components: {
    EbookReader,
    EbookTitle,
    EbookMenu
  },
  methods: {
    startLoopReadTime () {
      let readTime = getReadTime(this.fileName)
      // 初次进入
      if (!readTime) {
        readTime = 0
      }
      // 定时任务
      this.task = setInterval(() => {
        readTime++
        if (readTime % 30 === 0) {
          saveReadTime(this.fileName, readTime)
        }
      }, 1000)
    }
  },
  mounted () {
    this.startLoopReadTime()
  },
  beforeDestroy () {
    if (this.task) {
      // 终止定时任务
      clearInterval(this.task)
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  @import "../../assets/styles/global.scss"
</style>
