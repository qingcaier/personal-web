<template>
  <scroller :on-refresh="refresh" :on-infinite="infinite" ref="myscroller">
    <div class="home">
      <!-- <my-refresh :on-refresh="onRefresh">
      <my-reload
        :on-infinite-load="onInfiniteLoad"
        :parent-pull-up-state="infiniteLoadData.pullUpState"
      >-->

      <div class="form">
        <div class="formInner">
          <my-input class="inp" :label="'申请事项编号'" :value="value"></my-input>
          <my-input class="inp" :label="'申请开始时间'" :value="value1"></my-input>
          <my-input class="inp" :label="'事项名称'" :value="value2"></my-input>
          <my-input class="inp" :label="'结束时间'" :value="value3"></my-input>
          <div class="buttonArea">
            <div class="border">
              <div class="inner total">全部</div>
            </div>
            <div class="border cell">
              <div class="inner">在办</div>
              <div class="inner">不予兑现</div>
            </div>
            <div class="border cell">
              <div class="inner">已办结</div>
              <div class="inner">中止申请</div>
            </div>
          </div>
          <button class="search" type="button">查询</button>
        </div>
      </div>

      <div class="itemContain">
        <my-item
          class="itemLi"
          v-for="(item, idx) in arr"
          :key="idx"
          :order="item.order"
          :title="item.title"
          :num="item.num"
          :time="item.time"
          :count="item.count"
          :state="item.state"
        ></my-item>
      </div>
      <!-- </my-reload>
      </my-refresh>-->
    </div>
  </scroller>
</template>

<script>
// @ is an alias to /src
import item from '@/components/Item.vue'
import input from '@/components/Input.vue'
// import refresh from '@/components/DropDownRefresh.vue'
// import reload from '@/components/PullUpReload.vue'

const itemObj = [
  {
    order: '01',
    title: '投资促进局一事一议或一企一策的扶持奖金',
    num: 'TC20180904-010',
    time: '2018-08-04 15:55:09',
    count: '1:00',
    state: '预审不通过'
  },
  {
    order: '02',
    title: '招商单位引荐内资非用地项目奖励金',
    num: 'TC20180904-010',
    time: '2018-08-04 15:55:09',
    count: '0:00',
    state: '已拨付'
  },
  {
    order: '03',
    title: '上市企业管理团队招商奖励',
    num: 'TC20180904-010',
    time: '2018-08-04 15:55:09',
    count: '1:00',
    state: '通过预审'
  },
  {
    order: '04',
    title: '上市企业管理团队招商奖励',
    num: 'TC20180904-010',
    time: '2018-08-04 15:55:09',
    count: '1:00',
    state: '预审不通过'
  },
  {
    order: '04',
    title: '上市企业管理团队招商奖励',
    num: 'TC20180904-010',
    time: '2018-08-04 15:55:09',
    count: '1:00',
    state: '预审不通过'
  }
]
export default {
  name: 'Home',
  components: {
    'my-item': item,
    'my-input': input
    // 'my-refresh': refresh,
    // 'my-reload': reload
  },
  data() {
    return {
      value: '',
      value1: '',
      value2: '',
      value3: '',

      noDate: false, //这是一个判断是否加载的开关
      arr: [
        // {
        //   order: "01",
        //   title: "投资促进局一事一议或一企一策的扶持奖金",
        //   num: "TC20180904-010",
        //   time: "2018-08-04 15:55:09",
        //   count: "1:00",
        //   state: "预审不通过"
        // },
        // {
        //   order: "02",
        //   title: "招商单位引荐内资非用地项目奖励金",
        //   num: "TC20180904-010",
        //   time: "2018-08-04 15:55:09",
        //   count: "0:00",
        //   state: "已拨付"
        // },
        // {
        //   order: "03",
        //   title: "上市企业管理团队招商奖励",
        //   num: "TC20180904-010",
        //   time: "2018-08-04 15:55:09",
        //   count: "1:00",
        //   state: "通过预审"
        // },
        // {
        //   order: "04",
        //   title: "上市企业管理团队招商奖励",
        //   num: "TC20180904-010",
        //   time: "2018-08-04 15:55:09",
        //   count: "1:00",
        //   state: "预审不通过"
        // },
        // {
        //   order: "04",
        //   title: "上市企业管理团队招商奖励",
        //   num: "TC20180904-010",
        //   time: "2018-08-04 15:55:09",
        //   count: "1:00",
        //   state: "预审不通过"
        // }
      ],
      page: 1,
      pageSize: 4
    }
  },
  methods: {
    getData() {
      if (this.page * this.pageSize < itemObj.length) {
        this.arr = itemObj.slice(0, this.page * this.pageSize)
      } else {
        this.arr = itemObj
        this.noDate = true
      }
    },
    refresh() {
      this.page = 1 //重置页数刷新每次页数都是第一页
      this.noDate = false //重置数据判断

      setTimeout(() => {
        this.getData()
        this.$refs.myscroller.finishPullToRefresh() //刷新完毕关闭刷新的转圈圈
      }, 1700)
    },

    infinite(done) {
      if (this.noDate) {
        this.$refs.myscroller.finishInfinite(true)
      } else {
        setTimeout(() => {
          this.page++ //下拉一次页数+1
          this.getData()
          done() //进行下一次加载操作
        }, 1500)
      }
    }
  },
  mounted() {
    this.getData()
  }
}
</script>
<style lang="stylus" scoped>
.home {
  // position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .form {
    width: 94%;
    border: 1px solid lightgrey;
    border-radius: 1vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 4vw;
    padding-bottom: 4vw;

    .formInner {
      width: 90%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      .inp {
        margin-bottom: 1vw;
      }

      .buttonArea {
        width: 100%;
        height: 18vw;
        margin-top: 4vw;
        display: flex;
        justify-content: space-between;

        .border {
          width: 32%;
        }

        .inner {
          width: 98%;
          height: 8vw;
          border: 1px solid lightgrey;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 3vw;

          &:hover {
            color: rgb(50, 160, 205);
            border-color: rgb(50, 160, 205);
          }
        }

        .total {
          width: 98%;
          height: 17.6vw;
          border: 1px solid lightgrey;
        }

        .cell {
          display: flex;
          flex-direction: column;
          justify-content: space-between;
        }
      }
    }

    .search {
      width: 100%;
      height: 9vw;
      border: none;
      border-radius: 2px;
      background-color: rgb(50, 160, 205);
      color: white;
      margin-top: 4vw;
    }
  }

  .itemContain {
    width: 94%;
    margin-top: 4vw;

    .itemLi {
      margin-bottom: 2vw;
    }
  }
}
</style>
