<template>
  <div class="cart">
    <div class="cart-header">
      <div @click="$emit('cart-clicked')" >
        <button class="trolly">
          <img src="@/assets/img/shopping-cart.png">
        </button>
        <h1>Cart</h1>
        <div class="badge-cart">{{ cartSum }}</div>
      </div>
    </div>
    <div class="wrap-body">
      <div class="cart-body">
        <CardOnCart v-for="(item, i) in selected" :key="i"
                    :item="item" />
        <div v-if="isEmpty" class="empty-cart">
          <div class="empty-img">
            <img src="@/assets/img/empty-cart.png">
          </div>
          <h1>Your cart is empty</h1>
          <p>Please add some items from the menu</p>
        </div>
      </div>
    </div>
    <div class="cart-footer">
      <div class="cart-total">
        <div class="total-result">
          <p>Total:</p>
          <p>Rp. {{ $store.getters.sumTotal }}*</p>
        </div>
        <span>*Belum termasuk ppn</span>
      </div>
      <div class="cart-btn-group">
        <button @click="$emit('checkout-clicked')" class="btn btn-primary">Checkout</button>
        <button @click="$emit('cancel-clicked')" class="btn btn-secondary">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
import CardOnCart from '@/components/part/CardOnCart.vue'

export default {
  computed: {
    selected () {
      return this.$store.state.selected
    },
    isEmpty () {
      return this.selected.length === 0
    },
    cartSum () {
      return this.$store.state.cartSum
    }
  },
  components: {
    CardOnCart
  }
}
</script>

<style lang="scss" scoped>
.cart {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 3;
  background-color: white;
  width: 0vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  box-shadow: 4px 0 7px rgba(0, 0, 0, 0.733);
  overflow: hidden;
  transition: .3s;
  &.active {
    width: 25vw;
  }
}
.cart-header, .wrap-body {
  width: 100%;
}
.cart-header {
  padding: 12.5px 0;
  box-shadow: 0 -4px 7px rgba(0, 0, 0, 0.733);
  div {
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }
  .trolly {
    margin: 0 5px 0 0;
    background-color: transparent;
    border: none;
    cursor: pointer;
    img {
      height: 25px;
    }
  }
  h1 {
    font-size: 20px;
    font-weight: bold;
  }
  .badge-cart {
    width: 18px;
    height: 18px;
    border-radius: 15px;
    background-color: #57CAD5;
    color: white;
    margin-left: 4px;
    font-weight: 500;
    font-size: 15px;
    text-align: center;
    line-height: 18px;
  }
}
.wrap-body {
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow-y: auto;
  &::-webkit-scrollbar {
    width: 5px;
  }
  &::-webkit-scrollbar-thumb {
    background-color: #dbdbdb;
    border-radius: 10px;
  }
  &::-webkit-scrollbar-track {
    background-color: transparent;
    border-radius: 10px;
  }
  .cart-body {
    .empty {
      display: none;
    }
    .empty-cart {
      .empty-img {
        margin: 0 auto;
        width: 160px;
        height: 135px;
        overflow: hidden;
        img {
          width: 100%;
          object-fit: cover;
          background-position: center;
        }
      }
      h1 {
        font-size: 20px;
        font-weight: bold;
        margin-bottom: 4px;
      }
      p {
        font-size: 15px;
        font-weight: 400;
        color: #cecece;
      }
    }
  }
}
.cart-footer {
  display: flex;
  flex-direction: column;
  padding: 10px;
  margin-top: auto;
  .cart-total {
    padding: 0 5px;
    text-align: left;
    .total-result {
      display: flex;
      flex-wrap: nowrap;
      justify-content: space-between;
      margin-bottom: 4px;
      font-weight: bold;
    }
    span {
      font-size: 12px;
    }
  }
  .cart-btn-group {
    button {
      width: 100%;
      margin: 5px 0;
      padding: 6px 0;
      border-radius: 2px;
      cursor: pointer;
    }
  }
}
</style>
