<template>
  <div class="v-catalog-item">
    <img class="v-catalog-item__image"  :src=" require('../assets/images/'+ product_data.image)" alt="img">
    <p class="v-catalog-item__name">{{product_data.name}}</p>
    <p class="v-catalog-item__price">price:{{product_data.price }} P.</p>
    <button class="v-catalog-item__add_to_crad_bth bth"
            @click="addToCart">
      add to card
    </button>
  </div>

</template>

<script>

export default {
  name: "v-catalog-item",
  props: {
    product_data:{
      type: Object,
      default(){
        return {}
      }
    }
  },
  data() {
    return{}
  },
  computed: {},
  methods:{
    addToCart() {
      this.$emit('addToCart',this.product_data)
      }
  }
}
</script>

<style lang="scss">
@import '@/assets/styles/style.scss';
.v-catalog-item {
flex-basis: 25%;
  box-shadow: 0 0 8px 0 #e0e0e0;
  padding: $padding*2;
  margin-bottom: $margin*2;
  &__image{
  width: 100px;
    height: 100px;
}

}

</style>