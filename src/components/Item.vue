<template>
  <div class="item">
    <div class="order">{{ order }}</div>
    <div class="text">
      <div class="title">{{ title }}</div>
      <div class="mark">
        <span>{{ num }}</span>
        &nbsp;|&nbsp;
        <span>
          {{ time }}
        </span>
      </div>
    </div>
    <div class="state">
      <div>
        <span class="num">
          {{ count }}
        </span>
        <span class="yuan">元</span>
      </div>

      <div class="statemsg">
        {{ state }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Item",
  props: {
    order: String,
    title: String,
    num: String,
    time: String,
    count: String,
    state: String
  },
  data() {
    return {
      msg: "emmm"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.item {
  // width: 100vw;
  height: 22vw;
  display: flex;
  align-items: center;
  border: 1px solid lightgrey;
  justify-content: space-between;

  border-radius: 5px;

  .order {
    width: 6vw;
    height: 6vw;
    border-radius: 100%;
    background-color: lightgray;
    text-align: center;
    line-height: 6vw;
    font-size: 3vw;
    color: rgb(100, 100, 100);
    align-self: flex-start;
    margin-top 10px;
    margin-left: 10px;
 }

  .text{
    width: 60vw;
    height: 18vw;
    font-size: 4vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    .title{

    }

    .mark{
      min-width: 62vw;
      color: lightgrey;
      span{
        font-size: 5px;
      }
    }
  }

  .state{
    width:21vw;
    height: 18vw;
    background-color: rgb(50, 160, 205);
    font-size: 3vw;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items center
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;


    .num{
      font-size: 1.5em;
    }
    .yuan{
      font-size: 0.5em;
    }

  }
}
</style>
