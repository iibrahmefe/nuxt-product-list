<template>
  <div class="card">
    <h1 class="card-title">Desserts</h1>
    <div class="card-wrapper">
      <div class="card-item" v-for="item in desserts" :key="item.id">
        <img :src="item.image" alt="">
        <div class="desc">
          <p class="type">{{ item.type }}</p>
          <h2>{{ item.name }}</h2>
          <p class="price">${{ item.price }}</p>
        </div>
        <button class="add-to-basket" @click="addtoBasket(item)">Add to Cart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      desserts: [
        {
          id: 1,
          name: "Waffle with Berries",
          type: "Waffle",
          price: 6.50,
          image: require('~/assets/images/image-waffle-desktop.jpg')
        },
        {
          id: 2,
          name: "Vanilla Bean Crème Brûlée",
          type: "Crème Brûlée",
          price: 7.00,
          image: require('~/assets/images/image-creme-brulee-desktop.jpg')
        },
        {
          id: 3,
          name: "Macaron Mix of Five",
          type: "Macaron",
          price: 8.00,
          image: require('~/assets/images/image-macaron-desktop.jpg')
        },
        {
          id: 4,
          name: "Classic Tiramisu",
          type: "Tiramisu",
          price: 5.50,
          image: require('~/assets/images/image-tiramisu-desktop.jpg')
        },
        {
          id: 5,
          name: "Pistachio Baklava",
          type: "Baklava",
          price: 4.00,
          image: require('~/assets/images/image-baklava-desktop.jpg')
        },
        {
          id: 6,
          name: "Lemon Meringue Pie",
          type: "Pie",
          price: 5.00,
          image: require('~/assets/images/image-cake-desktop.jpg')
        },
        {
          id: 7,
          name: "Red Velvet Cake",
          type: "Cake",
          price: 4.50,
          image: require('~/assets/images/image-meringue-desktop.jpg')
        },
        {
          id: 8,
          name: "Salted Caramel Brownie",
          type: "Brownie",
          price: 4.50,
          image: require('~/assets/images/image-panna-cotta-desktop.jpg')
        },
        {
          id: 9,
          name: "Vanilla Panna Cotta",
          type: "Panna Cotta",
          price: 6.50,
          image: require('~/assets/images/image-brownie-desktop.jpg')
        }
      ],
      basket: []
    };
  },
  methods: {
    addtoBasket(item) {
      // Sepette ürün olup olmadığını kontrol et
      const existingItem = this.basket.find(b => b.id === item.id);

      if (existingItem) {
        existingItem.quantity += 1; // Ürün zaten sepette ise miktarı artır
      } else {
        // Ürün yeni ise sepete ekle ve miktarı 1 olarak ayarla
        this.basket.push({ ...item, quantity: 1 });
      }

      // Sepeti güncelle
      this.$emit('basket-updated', this.basket);
    }
  }
};
</script>


<style scoped>
  .card{
    padding: 40px 20px;
  width: 80%;
  display: grid;
  }


.card-title{
  font-size: 36px;
  font-weight: bold;
}

  .card-wrapper {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
  }
  
  .card-item {
    display: flex;
    border-radius: 8px;
    overflow:hidden ;
    position: relative;
    flex-direction: column;
    -webkit-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.1);
-moz-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.1);
box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.1);
transition: .2s;
filter: grayscale(30%);
  }

  .card-item:hover{
    -webkit-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.2);
-moz-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.2);
box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.2);
filter: grayscale(0%);
  }
  
  .add-to-basket{
    position: absolute;
    bottom: 75px;
    border-radius: 999px;
    max-width: 40%;
    margin: 0 auto;
    right: 0;
    left: 0;
    padding: 12px 6px;
    background: orange;
    color: white;
    border: 0;
    cursor: pointer;
  }


  .card-item img {
    width: 100%;
    height: auto; /* Yüksekliği otomatik ayarla */
    object-fit: cover;
  }
  
  .card-item .type{
    opacity: 60%;
  }

  .card-item .desc {
    padding: 10px;
    flex: 1; /* Genişliği otomatik ayarla */
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
   
  /* Responsive Tasarım */
  @media (max-width: 1024px) {
    .card-wrapper {
      grid-template-columns: repeat(2, 1fr); /* 2 sütun */
    }
  }
  
  @media (max-width: 768px) {
    .card-wrapper {
      grid-template-columns: 1fr; /* 1 sütun */
    }
  }
</style>