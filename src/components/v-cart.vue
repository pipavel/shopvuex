<template>
   <div class='v-cart'>
     <router-link :to="{name: 'catalog'}" >
       <div class="v-catalog_link_to_cart">Назад в карзину</div>
     </router-link>
    <H1>Корзина</H1>
     <p v-if="!cart_data.length">THE ARE PRODUCT</p>
 <v-cart-item
     v-for="(item, index) in cart_data"
     :key="item.article"
     :cart_item_data="item"
     @DeleteFromCard="DeleteFromCard(index)"
     @increment="increment(index)"
     @decrement="decrement(index)"
 />

     <div class="v-cart__total">
     <p class="total__name">Total:</p>
     <P>{{cartTotalCost}}</P></div>
   </div>

</template>

<script>
import vCartItem from './v-cart-item'
import  {mapActions} from  'vuex'

export default {
  name: "v-cart",
  components: {
    vCartItem
  },
  props: {
    cart_data: {
      type: Array,
      default() {
        return []
      }
    }
  },
  data() {
    return {}
  },
  computed: {
    cartTotalCost() {
      let result = []
      if (this.cart_data.length) {
        for (let item of this.cart_data) {
          result.push(item.price * item.quantity);
        }
        result = result.reduce(function (sum, el) {
          return sum + el;
        })
        return result
      } else {
        return 0
      }
    }
  },

  methods: {
    ...mapActions([
      'DELETE_FROM_CART',
      'INCREMENT_CART_ITEM',
      'DECREMENT_CART_ITEM'
    ]),
    increment(index){
this.INCREMENT_CART_ITEM(index)
    },
    decrement(index){
this.DECREMENT_CART_ITEM(index)
    },
    DeleteFromCard(index) {
      this.DELETE_FROM_CART(index)
    }
  }
}

</script>

<style lang="scss">
@import '@/assets/styles/style.scss';
.v-catalog_link_to_cart{
  position: absolute;
  top: 10px;
  right: 10px;
  padding: $padding*2;
  border: solid 1px #aeaeae;
}

.v-cart {
  margin-bottom: 100px;
  &__total {
    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;
    padding: $padding*3;
    display: flex;
    justify-content: center;
    background: #26ea88;
    color: #ffffff;
    font-size: 20px;
  }
  .total__name {
    margin-right: $margin*3;

  }
}

</style>