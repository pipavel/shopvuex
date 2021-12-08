<template>
<div class='v-cart-item'>
 <img class='v-cart-item__image' :src=" require('../assets/images/' + cart_item_data.image) " alt="">
  <div class='v-cart-item__info'>
    <p>{{cart_item_data.name}}</p>
    <p>{{cart_item_data.price}}</p>
    <p>{{cart_item_data.article}}</p>
  </div>
  <div class='v-cart-item__quantity'>
    <p>Qty:</p>
    <span class="quantity__btn" @click="decrementItem">-</span>
          {{cart_item_data.quantity}}
    <span class="quantity__btn" @click="incrementItem">+</span>

  </div>
  <button @click="DeleteFromCard"> delete</button>
</div>
</template>

<script>
export default {
name: "v-cart-item",
  props: {
  cart_item_data:{
    type: Object,
    default(){
      return{}
    }
  }
},
  data() {
  return {}
  },
  computed:{ },
  methods:{
      DeleteFromCard(){
      this.$emit('DeleteFromCard')
    },
    decrementItem(){
    this.$emit('decrement')
    },
    incrementItem(){
      this.$emit('increment')
    }

  },
  mounted() {
  this.$set(this.cart_item_data, 'quantity', 1)

  }
}
</script>

<style lang="scss">
@import '@/assets/styles/style.scss';
.v-cart-item {
display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 0 8px 0 #e0e0e0;
  padding: $padding*2;
  margin-bottom: $margin*2;
  &__image {
    height: 100px;
    width: 100px;
  }
  .quantity__btn{
    cursor: pointer;
  }
}
</style>