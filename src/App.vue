<template>
  <div class="page-wrap">
    <h3 class="check">結帳</h3>
    <router-view />
  </div>
</template>
<script>
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
import "@/assets/css/style.css";
// import stepNum from "./components/stepNum";
// import step1 from "./components/step1";
// import cart from "./components/cart";

export default {
  name: "App",
  components: {
    // stepNum,
    // step1,
    // cart,
  },
  data() {
    return {};
  },
};
</script>
