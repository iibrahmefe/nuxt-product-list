<template>
  <loading v-if="loading"/>
    <main v-else>
      <cards @basket-updated="updateBasket" />
      <basket :basket="basket" @remove-item="removeFromBasket" class="basket"/>
    </main>
</template>

<script>
export default {
  name: 'IndexPage',

  data() {
    return {
      basket: [],
      loading:true
    };
  },
  methods: {
    updateBasket(newBasket) {
      this.basket = newBasket; // Sepeti güncelle
    },
    removeFromBasket(item) {
      this.basket = this.basket.filter(i => i !== item); // Sepetten ürünü çıkar
    }
  },
  mounted(){
    setTimeout(()=>{
      this.loading=false
    },500)
  }
}
</script>

<style>

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-size: 16px;
  text-wrap: nowrap;
  
}
main{
  min-height: 100vh;
  max-width:1440px;
  width: 100%;
  margin: 0 auto;
  display: flex;
}



.basket{
  width: 20%;
}


</style>
