<template>
  <div class="page">
    <div class="check-gap">
      <div class="part-wrap w-100">
        <stepNum :partNo="partNo" />
        <step1 v-if="partNo === 0" />
        <step2
          v-else-if="partNo === 1"
          :initialShipWays="shipWays"
          @change-ship-way-id="changeShipWayId"
        />
        <step3 v-else-if="partNo === 2" />
      </div>
      <div class="btn-wrap d-flex justify-content-between">
        <button
          class="btn-pre d-flex align-items-center"
          @click.stop.prevent="partNum"
          v-if="partNo >= 1"
        >
          <img src="https://imgpile.com/images/5PdWou.png" alt="" class="pre" />
          上一步
        </button>
        <div class="" v-else></div>
        <button
          class="btn-next d-flex align-items-center"
          @click.stop.prevent="partNum"
          v-if="partNo <= 1"
        >
          下一步
          <img
            src="https://imgpile.com/images/5CYzQW.png"
            alt=""
            class="next"
          />
        </button>
        <button
          class="btn-next d-flex align-items-center"
          @click.stop.prevent="partNum"
          v-else
        >
          確認下單
          <img
            src="https://imgpile.com/images/5CYzQW.png"
            alt=""
            class="next"
          />
        </button>
      </div>
    </div>
    <cart
      :initialItems="items"
      :initialShipAmount="shipAmount"
      :initialTotal="total"
      :initialItemPrice="itemPrice"
      @add-items="addItemId"
      @minus-items="minusItemId"
    />
  </div>
</template>
<script>
import stepNum from "../components/stepNum";
import step1 from "../components/step1";
import step2 from "../components/step2";
import step3 from "../components/step3";
import cart from "../components/cart";
const dummyCart = {
  items: [
    {
      id: 1,
      name: "破壞補丁修身牛仔褲",
      price: 3999,
      quantity: 1,
      image: "https://upload.cc/i1/2022/03/25/n5MSYs.png",
    },
    {
      id: 2,
      name: "刷色直筒牛仔褲",
      price: 1299,
      quantity: 1,
      image: "https://upload.cc/i1/2022/03/25/tV6EMq.png",
    },
  ],
  shipAmount: 0,
  itemPrice: 0,
  total: 100,
};
const dummyShipAmount = {
  shipWays: [
    {
      id: 1,
      name: "標準運送",
      shipFee: 0,
      attention: "48 小時內送達",
      isChecked: true,
    },
    {
      id: 2,
      name: "DHL 貨運",
      shipFee: 500,
      attention: "約 3~7 個工作天",
      isChecked: false,
    },
  ],
};
export default {
  name: "home",
  components: {
    stepNum,
    step1,
    step2,
    step3,
    cart,
  },
  data() {
    return {
      partNo: 0,
      items: [],
      shipAmount: 0,
      total: 0,
      shipWays: [],
      initialShipWayId: "",
      itemPrice: 0,
    };
  },
  created() {
    this.fetchCart();
    this.fetchShipWays();
    // this.itemPriceAccount();
  },

  methods: {
    fetchCart() {
      const { items, shipAmount, total } = dummyCart;
      // const { id, name, price, quantity, image } = items;
      // this.items = { id, name, price, quantity, image }`;
      this.items = items;
      // this.shipAmount = shipAmount;
      this.shipAmount = shipAmount;
      this.total = total;
      //也可以這樣寫
      // this.items = dummyCart.items;
      // this.shipAmount = dummyCart.shipAmount;
      // this.total = dummyCart.total;
    },
    fetchShipWays() {
      const { shipWays } = dummyShipAmount;
      this.shipWays = shipWays;
    },
    partNum(e) {
      console.log(e.target);
      const step = e.target.classList;
      const part = document.querySelector(".part");
      if (step.contains("btn-pre") && this.partNo > 0) {
        console.log(5555);

        part.classList.remove("d-block");
        this.partNo = this.partNo - 1;
        part.classList.add("d-block");
        console.log(this.partNo);
      } else if (step.contains("btn-next") && this.partNo <= 1) {
        console.log(this.partNo);

        part.classList.remove("d-block");
        this.partNo = this.partNo + 1;
        part.classList.add("d-block");
        console.log(this.partNo);
      }
    },
    // itemPriceAccount() {
    //   console.log(this.itemPrice);
    //   this.itemPrice = this.items.map((item) => {
    //     return item.quantity * item.price;
    //   });
    // },
    addItemId(ItemId) {
      // console.log(ItemId);
      const currentItem = this.items.find((item) => item.id === Number(ItemId));
      // console.log(currentItem);
      currentItem.quantity = currentItem.quantity + 1;
    },
    minusItemId(ItemId) {
      // console.log(ItemId);
      const currentItem = this.items.find((item) => item.id === Number(ItemId));
      // console.log(currentItem);
      if (currentItem.quantity === 0) return;
      currentItem.quantity = currentItem.quantity - 1;
    },
    changeShipWayId(shipID) {
      this.initialShipWayId = Number(shipID);
      // console.log(this.initialShipWayId);
      const currentShip = this.shipWays.filter(
        (shipWay) => shipWay.id === shipID
      );
      this.shipAmount = currentShip[0].shipFee;
      // console.log(currentShip);
      console.log("currentShip", currentShip[0].shipFee);
    },
  },
  // watch: {
  //   items() {
  //     console.log(this.itemPrice);
  //     this.itemPrice = this.items.map((item) => {
  //       return item.quantity * item.price;
  //     });
  //   },
  // },
};
</script>
