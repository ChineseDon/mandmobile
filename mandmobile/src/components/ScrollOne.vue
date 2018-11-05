<template>
  <div class="container">
    <md-scroll-view
      ref="scrollView"
      :scrolling-x="false"
      @scroll="scroll">
      <div>
        <div style="height: 1200px;">
          123
        </div>
        <div>
          456
        </div>
      </div>
    </md-scroll-view>
  </div>
</template>

<script>
  import {ScrollView} from 'mand-mobile'
  export default {
    name: "Scroll",
    mounted() {
      window.ScrollViewTrigger1 = () => {
        this.$refs.scrollView.triggerRefresh()
      }
      console.log(this.$refs.scrollView)
    },
    methods: {
      scroll(x) {
        console.log(x)
      }
    },
    components: {
      [ScrollView.name]: ScrollView,
    }
  }
</script>

<style scoped>
.container {
  width: 100%;
}
</style>
