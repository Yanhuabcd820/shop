<template>
  <div class="part ship-way">
    <h4>運送方式</h4>
    <div class="ship-way-wrap">
      <label
        class="ship-way d-flex justify-content-between"
        for="ship-stander"
        v-for="initialShipWay in initialShipWays"
        :key="initialShipWay.id"
      >
        <input
          type="radio"
          name="ship"
          :id="initialShipWay.id"
          :value="initialShipWay.id"
          v-model="ShipWayPicked"
          :check="ShipWayPicked === initialShipWay.id"
        />
        <div class="ship-content">
          <b>{{ initialShipWay.name }}</b>
          {{ initialShipWay.attention }}
        </div>
        <b class="ship-fee">
          {{ initialShipWay.shipFee | priceDeco }}
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
      shipWays: [],
      ShipWayPicked: "",
    };
  },
  created() {},
  methods: {},
  computed: {},
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
