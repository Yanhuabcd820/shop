<template>
  <div class="check-cart">
    <h4 class="shopping-list">購物籃</h4>
    <div class="list d-flex" v-for="Item in Items" :key="Item.id">
      <div class="list-pic">
        <img :src="Item.image" alt="" />
      </div>
      <div class="list-content d-flex justify-content-between">
        <div class="item-detail">
          <h5 class="item-name">{{ Item.name }}</h5>
          <div class="item-number d-flex justify-content-between">
            <div
              class="btn-quantity btn-minus"
              @click.prevent.stop="minusItem(Item.id)"
            >
              <span class="minus">&#8722;</span>
            </div>
            <div class="quantity">{{ Item.quantity }}</div>
            <div
              class="btn-quantity btn-add"
              @click.prevent.stop="addItem(Item.id)"
            >
              <span class="add">&#43;</span>
            </div>
          </div>
        </div>
        <div class="item-price">{{ Item.price | priceDeco }}</div>
      </div>
    </div>

    <div class="ship-fee d-flex justify-content-between">
      <div>運費</div>
      <b class="ship-amount">{{ initialShipAmount | priceDeco }}</b>
    </div>
    <div class="ship-fee d-flex justify-content-between">
      <div>小計</div>
      <b class="total">{{ (initialShipAmount + itemPrice) | priceDeco }}</b>
    </div>
  </div>
</template>
<script>
export default {
  name: "cart",
  props: {
    initialItems: {
      type: Array,
      required: true,
    },
    initialShipAmount: {
      type: Number,
      default: 0,
    },
    initialTotal: {
      type: Number,
      default: 0,
    },
    initialItemPrice: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      quantity: "",
      Items: [],
      shipAmount: 0,
      total: 0,
      itemPrice: 0,
    };
  },
  created() {
    this.fetchQuantity();
  },
  methods: {
    fetchQuantity() {
      this.Items = this.initialItems;
      this.quantity = this.initialItems;
      this.shipAmount = this.initialShipAmount;
      this.total = this.initialTotal;
      this.itemPrice = this.initialItemPrice;
      console.log("shipAmount", this.shipAmount);
    },
    addItem(addItemId) {
      this.$emit("add-items", addItemId);
    },
    minusItem(minusItemId) {
      this.$emit("minus-items", minusItemId);
    },
  },
  watch: {
    Items: {
      handler: function () {
        let itemPrice = 0;
        this.initialItems.forEach((item) => {
          itemPrice = itemPrice + item.quantity * item.price;
          return itemPrice;
        });
        console.log("money", itemPrice);
        this.itemPrice = itemPrice;
      },
      deep: true,
    },
    shipAmount: {
      handler: function () {
        console.log(555);
      },
    },
  },
  filters: {
    priceDeco(price) {
      if (price === 0) {
        return `免費`;
      }
      return `$${price.toLocaleString("en-US")}`;
    },
  },
};
</script>
