<template>
  <div class="part ship-way">
    <h4>運送方式</h4>
    <div class="ship-way-wrap">
      <label
        class="ship-way d-flex justify-content-between"
        :for="shipWay.id"
        v-for="shipWay in shipWays"
        :key="shipWay.id"
      >
        <input
          type="radio"
          name="ship"
          :id="shipWay.id"
          :value="shipWay.id"
          v-model="ShipWayPicked"
          :checked="shipWay.id === ShipWayPicked"
        />
        <div class="ship-content">
          <b>{{ shipWay.name }}</b>
          {{ shipWay.attention }}
        </div>
        <b class="ship-fee">
          {{ shipWay.shipFee | priceDeco }}
        </b>
      </label>
    </div>
  </div>
</template>
<script>
export default {
  name: "step2",
  props: {
    initialShipWays: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      shipWays: this.initialShipWays,
      ShipWayPicked: 1,
    };
  },

  filters: {
    priceDeco(price) {
      if (price === 0) {
        return `免費`;
      }
      return `$${price.toLocaleString("en-US")}`;
    },
  },
  watch: {
    ShipWayPicked() {
      this.$emit("change-ship-way-id", this.ShipWayPicked);
    },
  },
};
</script>
