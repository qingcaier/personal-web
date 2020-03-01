<template>
  <div class="input">
    <div class="label">{{ label }}</div>
    <input class="content" type="text" :value="value" />
  </div>
</template>

<script>
export default {
  name: "Item",
  props: {
    label: String,
    value: String
  },
  data() {
    return {};
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.input{
    width: 100%;
    display: flex;


    .label{
        width: 20vw;
        height: 8vw;
        line-height: 8vw;
        text-align: right
        font-size: 2vw;
        color: lightgrey;
        min-width : 100px;
    }

    .content{
        height: 8vw;
        width: 60vw;
        margin-left: 3vw;
        background-color: rgba(225 225 225 0.8)
        border: none
        padding-left: 4vw;
        font-size: 4vw;
        border-radius: 2px;

        &:focus{
          outline:none
        }
    }
}
</style>
