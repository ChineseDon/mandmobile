<template>
  <div class="container" @touchmove.prevent>
    <md-scroll-view
      ref="scrollView"
      :scrolling-x="false"
      :scrolling-y="true"
      @scroll="$_onScroll"
      @refreshing="$_onRefresh"
    >
      <md-scroll-view-refresh
        slot="refresh"
        slot-scope="{ scrollTop, isRefreshActive, isRefreshing }"
        :scroll-top="scrollTop"
        :is-refreshing="isRefreshing"
        :is-refresh-active="isRefreshActive"
      ></md-scroll-view-refresh>

      <div class="single-sycle">
        <div class="activity-item"  v-for="index in 10" :key="index" @click="detail">
          <div class="border-1px"></div>

          <div class="clear-result">
            <ul>
              <li>
                <p>￥20.00</p>
                <p>站点活动金</p>
              </li>
              <li v-if="index%2==0">
                <p>￥20.00</p>
                <p>站点保底</p>
              </li>
              <li>
                <p>￥0.00</p>
                <p>活动中奖</p>
              </li>
            </ul>
          </div>

          <ul class="pay-info" v-if="index%2!=0">
            <li>
              <p>收入</p>
              <p>用户参与金：<span class="userjoin">￥20.00</span></p>
            </li>
            <li>
              <p>支出</p>
              <p>赏金：<span class="prize">￥0.00</span></p>
            </li>
          </ul>

          <div class="money" v-if="index%2==0">
            <div class="income">
              <div class="name">收入</div>
              <div class="data">
                <p>用户参与金：<span>￥8.00</span></p>
                <p>他站分成收益：<span>￥8.00</span></p>
              </div>
            </div>
            <div class="outPay">
              <div class="name">支出</div>
              <div class="data">
                <p>赏金：<span>￥8.00</span></p>
                <p>他站分成：<span>￥8.00</span></p>
                <p>发起者佣金：<span>￥8.00</span></p>
              </div>
            </div>
          </div>

          <ul class="activity-status">
            <li>活动金：<span class="award">￥20</span></li>
            <li>待出票</li>
          </ul>
        </div>
      </div>
      <md-scroll-view-more
        slot="more"
        :is-finished="isFinished"
      >
      </md-scroll-view-more>
    </md-scroll-view>

    <md-image-viewer
      v-model="isShow"
      :list="img"
      :has-dots="true"
      :initial-index="index">
    </md-image-viewer>
  </div>
</template>

<script>
  import {ScrollView, ScrollViewRefresh, ScrollViewMore, ImageViewer} from 'mand-mobile'

  export default {
    name: "HelloWorld",
    data () {
      return {
        probeType: 3,
        isShow: false,
        isFinished: true,
        index: 0,
        img: [
          'http://img-hxy021.didistatic.com/static/strategymis/insurancePlatform_spu/uploads/27fb7f097ca218d743f816836bc7ea4a',
          'http://manhattan.didistatic.com/static/manhattan/insurancePlatform_spu/uploads/c2912793a222eb24b606a582fd849ab7',
          'http://img-hxy021.didistatic.com/static/strategymis/insurancePlatform_spu/uploads/6ee5a0ba9340ca452cbc827902e76be0',
          'http://img-hxy021.didistatic.com/static/strategymis/insurancePlatform_spu/uploads/d751dd4487e265de3b8587f504eee2c3',
        ],
      }
    },
    mounted() {
      console.log(this.$refs.scrollView)
    },
    created () {
      this.$nextTick(() => {
        // this.$router.go(0)
        console.log(879)
        this.$refs.scrollView.reflowScroller()
      })

    },
    methods: {
      search(e) {
        alert(e)
      },
      detail () {
        this.$router.push({
          path: '/ticketSSQDetail'
        })
      },
      showViewer() {
        this.index = 0;
        this.isShow = true;
      },
      $_onScroll (x) {
        // console.log(x)
      },
      $_onRefresh() {
        console.log(123)
      }
    },
    components: {
      [ScrollView.name]: ScrollView,
      [ScrollViewRefresh.name]: ScrollViewRefresh,
      [ScrollViewMore.name]: ScrollViewMore,
      [ImageViewer.name]: ImageViewer,
    }
  }
</script>

<style scoped>
  .container {
    width: 100%;
  }
  .single-sycle {
    width: 100%;
    padding-top: 20px;
    box-sizing: border-box;
    background-color: #f4f4f4;;
  }
  .activity-item {
    width: 703px;
    padding: 30px 0 30px 30px;
    margin: 20px auto 0 auto;
    background-color: #ffffff;
    border-radius: 16px;
    box-sizing: border-box;
    font-size: 0;
  }
  .border-1px {
    position: relative;
    width: 100%;
    margin-top: 20px;
  }
  .border-1px:after {
    content: '';
    position: absolute;
    left: 0;
    right: 30px;
    height: 1px; /* no */
    background-color: #e0e0e0;
    box-sizing: border-box;
  }

  .clear-result {
    display: flex;
    width: 643px;
    height: 120px;
    padding-top: 30px;
    box-sizing: border-box;
  }
  .clear-result > ul {
    display: flex;
    width: 100%;
    height: 70px;
  }
  .clear-result > ul > li {
    display: flex;
    flex-direction: column;
    flex: 1;
    text-align: center;
  }
  .clear-result > ul > li > p {
    flex: 1;
    height: 50%;
    font-size: 28px;
    color: #333333;
  }
  .clear-result > ul > li > p:first-child {
    font-weight: 500;
  }
  .clear-result > ul > li > p:last-child {
    font-size: 24px;
    color: #999999;
  }

  .pay-info {
    display: flex;
    flex-direction: column;
    width: 643px;
    height: 132px;
    background-color: #f3f3f3;
    border-radius: 16px;
  }
  .pay-info > li {
    display: flex;
    flex: 1;
    align-items: center;
    margin: 0 24px;
  }
  .pay-info > li:first-child {
    border-bottom: 1px solid #e0e0e0;
  }
  .pay-info > li > p:first-child {
    flex: 1;
    color: #333333;
    font-size: 28px;
  }
  .pay-info > li > p:last-child {
    font-size: 20px;
    color: #999999;
  }
  .userjoin, .prize {
    font-size: 28px;
  }
  .userjoin {
    color: #00c503;
  }
  .prize {
    color: #ff0000;
  }
  .activity-status {
    display: flex;
    font-size: 0;
    margin: 30px 30px 0 0;
  }
  .activity-status > li {
    flex: 1;
    height: 30px;
    color: #333333;
    font-size: 28px;
  }
  .activity-status > li:last-child {
    text-align: right;
  }

  .money {
    width: 642px;
    height: 247px;
    padding: 0 20px;
    background-color: #f3f3f3;
    border-radius: 16px;
    box-sizing: border-box;
  }
  .income,
  .outPay {
    display: flex;
    width: 100%;
  }
  .income {
    height: 100px;
    border-bottom: 1px solid #e0e0e0;
  }
  .income > .name,
  .outPay > .name {
    flex: 1;
    font-size: 28px;
    color: #333333;
    text-align: left;
    padding: 20px 0;
  }
  .income > .data,
  .outPay > .data {
    display: flex;
    flex-direction: column;
    flex: 3;
    padding-top: 8px;
    font-size: 20px;
    color: #999999;
  }
  .outPay {
    height: 150px;
  }
  .income > .data > p,
  .outPay > .data > p {
    width: 100%;
    height: 40px;
    line-height: 40px;
    text-align: right;
  }
  .data > p > span {
    font-size: 28px;
  }
  .income > .data > p > span {
    color: #00c503;
  }
  .outPay > .data > p > span {
    color: #ff0000;
  }

</style>
