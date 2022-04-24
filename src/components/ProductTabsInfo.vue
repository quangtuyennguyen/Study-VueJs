<template>
  <div class="container-fluid">
    <div class="col-md-12 product-info">
      <ul id="myTab" class="nav nav-tabs nav_tabs">
        <li
          v-for="(item, index) in tabs"
          :key="index"
          :class="{ active: index === tabIndex }"
        >
          <a
            @click="setTab(index, item.val)"
            href="#service-one"
            data-toggle="tab"
            >{{ item.name }}</a
          >
        </li>
      </ul>
      <div id="myTabContent" class="tab-content">
        <div class="tab-pane in active" id="service-one">
          <section v-html="tabContent" class="container product-info" />
        </div>
        <div class="tab-pane" id="service-two">
          <section class="container"></section>
        </div>
        <div class="tab-pane" id="service-three"></div>
      </div>
      <hr />
    </div>
  </div>
</template>

<script>
import { PRODUCT_TABS } from "../constants/index";
export default {
  props: {
    content: String,
    productInfo: String,
    review: String,
  },
  data() {
    return {
      tabIndex: 0,
      tabContent: this.content,
      tabs: PRODUCT_TABS,
    };
  },
  methods: {
    setTab(index, content) {
      this.tabContent = this[content];
      return (this.tabIndex = index);
    },
  },
};
</script>

<style lang="css" scoped>
.nav-tabs .active {
  border: 2px solid #333;
}
</style>
