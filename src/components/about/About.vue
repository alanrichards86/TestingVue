<template>
  <div class="about">
 <div id="app" class="container">
    <div class="cart">
      <p class="cart-text" v-if="cartStatus()">You have {{ itemsInCart }} bottles in your cart</p>
      <p class="cart-text_empty" v-else>Your cart is empty</p>
      <button v-if="itemsInCart > 0" class="button-cart_primary">Go to checkout</button>
      <button @click="emptyCart" v-if="itemsInCart > 0" class="button-cart_secondary">Empty cart</button>
    </div>
    <div class="item">
      <img src="https://images.unsplash.com/photo-1506277789875-529f12691361?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=d708b98eaaa2379bb6d3c8d40240ce5c&auto=format&fit=crop&w=1296&q=60" alt="product-image" class="item-image">
      <div class="item-section">
        <div>
          <h3 class="item-title">Confused Duck drink</h3>
          <p class="item-meta">530 ml</p>
          <p class="item-meta">{{ itemsInStock }} items left in stock</p>
        </div>
        <span class="item-price">€ 4.99</span>
      </div>
      <p class="item-description">Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe vero quos non veniam quaerat . Soluta, repudiandae incidunt! Ullam, autem tenetur!</p>
      <div class="quantity">
        <button class="button-quantity" @click="quantity--" :disabled="quantity < 1">-</button>
        <input type="number" class="quantity-input" v-model="quantity">
        <button class="button-quantity" @click="quantity++" :disabled="quantity >= itemsInStock">+</button>
      </div>
      <button class="button-order" @click="addItemToCart" :disabled="itemsInStock == 0 || quantity == 0 || quantity > itemsInStock">Add to cart</button>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Cart',

  data () {
    return {
    itemsInCart: 0,
    itemsInStock: 5,
    quantity: 1
    }
  },
  methods: {
    addItemToCart() {
      if (this.itemsInStock > 0) {
        this.quantity = parseInt(this.quantity)
        this.itemsInCart += this.quantity
        this.itemsInStock -= this.quantity
        this.quantity = 0
      }
    },
    cartStatus() {
      if (this.itemsInCart > 0) {
        return true
      } else {
        return false
      }
    },
    emptyCart() {
      this.itemsInStock = this.itemsInStock + this.itemsInCart
      this.itemsInCart = 0
    }
  }

}
</script>

<style scoped>

:root {
  --color-text: #6C727D;
  --color-main: #FF3A52;
  --color-bg: #F2F4F5;
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Montserrat', sans-serif;
  background: #143040;
}

.container {
  width: 90%;
  max-width: 360px;
  margin: 0 auto;
  padding: 40px 0;
}

.cart {
  margin-bottom: 24px;
  background: var(--color-bg);
  padding: 16px;
  border-radius: 3px;
}

.cart-text {
  margin: 0 0 12px;
  color: var(--color-text);
  font-size: 14px;
  font-weight: 500;
  line-height: 21px;
}

.cart-text_empty {
  margin: 0;
  color: var(--color-text);
  font-size: 14px;
  font-weight: 500;
  line-height: 21px;
}

.item {
  background: var(--color-bg);
  padding: 16px 16px 48px;
  border-radius: 3px;
}

.item-image {
  width: 100%;
  height: auto;
  display: block;
  margin-bottom: 16px;
}

.item-section {
  margin-bottom: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgba(108, 114, 125, .3);
  padding-bottom: 16px;
}

.item-title {
  margin: 0 0 4px;
  font-size: 16px;
  font-weight: 600;
}

.item-meta {
  margin: 0;
  font-weight: 500;
  color: var(--color-text);
  font-size: 14px;
  opacity: .5;
}

.item-price {
  font-weight: 500;
  font-size: 24px;
  color: var(--color-main);
}

.item-description {
  margin: 0 0 16px;
  color: var(--color-text);
  font-size: 14px;
  font-weight: 500;
  line-height: 21px;
}

.quantity-input::-webkit-inner-spin-button,
.quantity-input::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.quantity {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 32px;
}

.quantity-input {
  width: 36px;
  height: 36px;
  text-align: center;
  border-radius: 3px;
  border: 1px solid #929CAA;
  font-size: 16px;
  margin: 0 16px;
  color: var(--color-text);
}

.quantity-show {
  margin: 0 0 32px;
  color: var(--color-text);
  font-size: 14px;
  font-weight: 500;
  line-height: 21px;
}

.button-quantity {
  background: var(--color-bg);
  border: none;
  border-radius: 50%;
  font-size: 24px;
  padding: 7px 13px;
  cursor: pointer;
  color: var(--color-text);
  outline: none;
}

.button-quantity:disabled {
  opacity: .2;
}

.button-order {
  display: block;
  width: 100%;
  max-width: 200px;
  margin: 0 auto;
  background: var(--color-main);
  border: 1px solid var(--color-main);
  color: black;
  border-radius: 24px;
  padding: 12px 0;
  font-size: 16px;
  box-shadow: 0 2px 4px rgba(0,0,0,.18);
  text-shadow: 0 1px 2px rgba(0,0,0,.2);
  cursor: pointer;
  outline: none;
}

.button-order:disabled {
  opacity: .4;
  cursor: not-allowed;
}

.button-cart_primary {
  background: var(--color-main);
  color: black;
  border: 1px solid var(--color-main);;
  border-radius: 16px;
  font-size: 14px;
  padding: 6px 12px;
  cursor: pointer;
  outline: none;
  box-shadow: 0 2px 4px rgba(0,0,0,.18);
  text-shadow: 0 1px 2px rgba(0,0,0,.2);
}

.button-cart_secondary {
  color: var(--color-text);
  background: transparent;
  border: none;
  font-size: 13px;
  cursor: pointer;
  outline: none;
  padding: 7px 12px;
  letter-spacing: .5px;
  opacity: .8;
}

.button-cart_secondary:hover {
  background: #E5E7EA;
  border-radius: 16px;
}

@keyframes loading {
  0% {
    flex-grow: 0;
    opacity: 0;
  }
  100% {
    flex-grow: 4;
    opacity: 1;
  }
}

</style>