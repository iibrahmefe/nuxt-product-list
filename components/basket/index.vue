<template>
  <div class="basket">
    <h2 class="basket-title">Your Cart ({{ basket.length }})</h2>
    <div class="basket-list ">
      <div v-for="item in basket" :key="item.id" class="basket-list-item">
        <div class="basket-item-left">
          <p>{{ item.name }}</p>
          <div class="basket-item-desc">
            <p>{{ item.quantity }}x</p>
            <p>${{ item.price }}</p>
            <p>${{ item.price * item.quantity }}</p>
          </div>
        </div>
        <div class="basket-item-right">
          <button class="remove-button" @click="removeFromBasket(item)">x</button>
        </div>
      </div>
    </div>
   <p class="bottom">${{ totalPrice }} </p>
  </div>
</template>

<script>
export default {
  data(){
    return{
      
    }
  },
  props: ['basket'], // Sepet verisini prop olarak al
  methods: {
    removeFromBasket(item) {
      // Sepetten ürünü çıkar ve sepetteki diğer ürünlerin miktarlarını güncelle
      const index = this.basket.findIndex(i => i.id === item.id);
      
      if (index !== -1) {
        if (this.basket[index].quantity > 1) {
          this.basket[index].quantity -= 1; // Miktarı azalt
        } else {
          this.basket.splice(index, 1); // Miktar 0 ise ürünü sepetten çıkar
        }
      }
      this.$emit('basket-updated', this.basket); // Parent bileşene sepetteki güncellemeleri bildir
    },
  
  },
  computed:{
    totalPrice(){
      return this.basket.reduce((total,item)=>{
        return total+(item.price*item.quantity);
      },0).toFixed(2);
    }
  }
};
</script>

<style scoped>
.basket{
position: sticky;
top: 40px;
padding: 40px 20px;
-webkit-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.1);
-moz-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.1);
box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.1);
height: max-content;
min-height: 500px;
max-height: 500px;
overflow: auto;
}
.basket-title{
    font-weight: bold;
    font-size: 24px;
    color: orange;
}
.basket-list-item{
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid gray;
}

.basket-item-desc{
    display: flex;
    gap: 5px;
}

.basket-item-desc p{
    font-size: 14px;
    opacity:70%;
    margin-top: 5px;
}

.remove-button{
    width: 20px;
    border-radius: 999px;
    height: 20px;
    background: #000;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    border: 0;
    outline: 0;
}

.bottom{
  position: absolute;
  bottom: 10px;
  left: 20px;
  font-size: 24px;
}
</style>