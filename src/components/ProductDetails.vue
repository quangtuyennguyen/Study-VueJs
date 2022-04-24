<template>
  <div class="item-container">
    <div class="container">
      <div class="col-md-8">
        <div class="row">
          <div class="product col-md-8 service-image-left">
            <div>
              <img id="item-display" :src="selectedVariant.image" alt="" />
            </div>
          </div>
          <div class="container service1-items col-md-4 pull-left">
            <div>
              <a
                @click="() => changeSelectedProduct(item)"
                :id="`item-${index + 1}`"
                v-for="(item, index) of product.variants"
                :key="item.id"
                class="service1-item"
              >
                <img
                  :style="{ width: '130px', height: '130px' }"
                  :src="item.image"
                  :alt="`${product.description} ${index + 1}`"
                />
              </a>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-7">
        <div class="product-actions">
          <div class="product-title">{{ product.title }}</div>
          <div class="product-desc">
            {{ product.description }}
          </div>
          <div class="product-rating">
            <font-awesome-icon
              v-for="i in 5"
              :key="i"
              :icon="
                product.rating >= i
                  ? 'fa fa-star gold'
                  : 'fa-solid fa-star-of-david'
              "
            />
          </div>
          <hr />
          <div class="product-price">
            {{ formatPrice(selectedVariant.price) }}
          </div>
          <span>Cart: {{ cart }}</span>
          <div v-if="selectedVariant.quatity > 0" class="product-stock">
            In Stock ({{ selectedVariant.quatity }})
          </div>
          <div v-else class="product-stock">Out of Stock</div>
          <hr />
          <div class="btn-group cart">
            <button @click="addToCart" type="button" class="btn btn-success">
              Add to cart
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { formatPrice } from "../utils/index";

export default {
  name: "ProductDetails",
  props: {
    product: Object,
  },
  data() {
    return {
      selectedVariant: this.product.variants[0] || {},
      cart: 0,
    };
  },
  methods: {
    changeSelectedProduct(variant) {
      return (this.selectedVariant = variant);
    },
    addToCart() {
      const { quatity } = this.selectedVariant;
      if (quatity > 0) {
        this.selectedVariant.quatity -= 1;
        return (this.cart += 1);
      }
      return alert("No product exist");
    },
  },
  computed: {
    formatPrice: () => (price) => {
      return formatPrice(price);
    },
  },
};
</script>

<style lang="css" scoped>
.product {
  border: 1px solid #dddddd;
}

.product-actions {
  margin-top: 20px;
}

.product > img {
  max-width: 230px;
}

.product-rating {
  font-size: 20px;
  margin-bottom: 25px;
}

.product-title {
  font-size: 20px;
}

.product-desc {
  font-size: 14px;
}

.product-price {
  font-size: 22px;
}

.product-stock {
  color: #74df00;
  font-size: 20px;
  margin-top: 10px;
}

.product-info {
  margin-top: 50px;
}

.service1-items {
  padding: 0px 0 0px 0;
  overflow: hidden;
  max-width: 100%;
  height: 321px;
  width: 130px;
}

.service1-item {
  height: 107px;
  width: 120px;
  display: block;
  float: left;
  position: relative;
  padding-right: 20px;
  border-right: 1px solid #ddd;
  border-top: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
}

.service1-item > img {
  max-height: 110px;
  max-width: 110px;
  opacity: 0.6;
  transition: all 0.2s ease-in;
  -o-transition: all 0.2s ease-in;
  -moz-transition: all 0.2s ease-in;
  -webkit-transition: all 0.2s ease-in;
}

.service1-item > img:hover {
  cursor: pointer;
  opacity: 1;
}

.service-image-left {
  padding-right: 50px;
}

.service-image-right {
  padding-left: 50px;
}

.service-image-left > center > img,
.service-image-right > center > img {
  max-height: 155px;
}
</style>
