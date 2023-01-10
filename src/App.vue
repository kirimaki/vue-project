<template>

  <Transition name="fade">
    <Modal @closeModal="ModalOpen(false)"
           :products="products"
           :choice="choice"
           :isModalOpen="isModalOpen" />
  </Transition>
      <div class="menu">
    <a v-for="(menuName,i) in menu" :key='i'>{{menuName}}</a>
  </div>

  <Discount :value="rate" @transData="transData($event)" v-if="isShowDiscount === true"/>

  <button v-if="isUpsort === true" @click="priceSort('up'); isUpsort=false;">가격순 오름 정렬</button>
  <button v-else @click="priceSort('down'); isUpsort=true;">가격순 내림 정렬</button>
  <button v-if="isCharUpsort === true" @click="charSort('up'); isCharUpsort=false;">가나다 오름 정렬</button>
  <button v-else @click="charSort('down'); isCharUpsort=true;">가나다 내림 정렬</button>
  <button @click="sortBack();">되돌리기</button>


  <Card @openModal="ModalOpen(true, $event)" @heartAdd="heartAdd($event)" v-for="(product,i) in products" :key="product" :product="products[i]" :heartCount="heartCount[i]"/>
  <button v-on:click="heartShot();">하트뿅뿅</button>
  <span id="heart">{{heartSpan}}</span>

</template>

<script>

import productData from './assets/product.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from "./Card.vue";

export default {
  name: 'App',
  data() {
    return {
      productsOrigin : [...productData],
      menu : ['Home', 'Products', 'About', 'Help'],
      products : productData,
      heartCount : [0, 0, 0, 0, 0, 0],
      heartSpan : "",
      isModalOpen : false,
      choice : 0,
      isUpsort : true,
      isCharUpsort : true,
      isShowDiscount : true,
      rate : 0
    }
  },
  methods : {
    heartAdd(index) {
      this.heartCount[index] += 1;
    },
    heartShot() {
      this.heartSpan += "♥";
    },
    ModalOpen(toggle, index) {
      this.isModalOpen = toggle;
      this.choice = index;
    },
    priceSort(type) {
      this.products.sort(function(a, b) {
        return (type === 'up' ? b.price - a.price : a.price - b.price)
      })
    },
    charSort(type) {
      this.products.sort(function(a, b) {
        console.log(b.title.charCodeAt(0));
        return (type === 'up' ? b.title.charCodeAt(0) - a.title.charCodeAt(0) : a.title.charCodeAt(0) - b.title.charCodeAt(0))
      })
    },
    sortBack() {
      return this.products = [...this.productsOrigin];
    },
    transData(value) {
      this.rate = value;
    }
  },
  mounted() {
    const test = setInterval(() => {
      if(this.rate > 0) {
        this.rate--;
      } else {
        clearInterval(test);
      }
    }, 1000)
  },
  components: {
    Card,
    Modal,
    Discount,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding:15px;
  border-radius: 5px;
}

.menu a {
  color : white;
  padding: 10px;
}

#heart {
  color : red;
}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

.fade-enter-from {
  transform: translateX(-1000px);
}
.fade-enter-active {
  transition: all 0.5s;
}
.fade-enter-to {
  transform: translateX(0px);
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

</style>
