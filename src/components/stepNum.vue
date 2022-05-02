<template>
  <div class="step-wrap w-100 d-flex justify-content-between">
    <div class="step d-flex active" :class="{ checked: partNo >= 1 }">
      <div class="step-circle"></div>
      <div class="step-line"></div>
      <div class="step-label">寄送地址</div>
    </div>
    <div
      class="step d-flex"
      :class="[{ active: partNo > 0 }, { checked: partNo > 1 }]"
    >
      <div class="step-circle"></div>
      <div class="step-line"></div>
      <div class="step-label">運送方式</div>
    </div>
    <div class="step d-flex" :class="{ active: partNo === 2 }">
      <div class="step-circle"></div>
      <div class="step-label">付款資訊</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "stepNum",
  props: {
    partNo: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      HY: 0,
    };
  },
  methods: {},
  // computed: {
  //   test() {
  //     // console.log(this.partNo);
  //     // alert(this.partNo);
  //     HY = 5;
  //   },
  // },
};
</script>
