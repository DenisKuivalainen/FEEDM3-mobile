<template>
  <view>
    <touchable-opacity class="row"
        :on-press="pressItem"
    >
        <text class="text">
            {{topic}}
        </text>
    </touchable-opacity>
  </view>
</template>

<script>
export default {
  props: {
    topic: {type: String},
    aidi: {type: Number},
    removeTodo: {type: Function}
  },
  methods: {
    pressItem: function() {
        this.$emit('setRecp', this.aidi)
    },
  }
};
</script>

<style>
  .row {
    background-color: rgb(217, 231, 240);
    border-radius: 10;
    justify-content: center;
    padding: 10;
    margin-bottom: 10;
  }
    .text {
        font-size: 15;
    }
</style>