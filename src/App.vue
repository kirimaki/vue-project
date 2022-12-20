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

  <Discount/>

  <button>가격순 정렬 버튼</button>

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
      menu : ['Home', 'Products', 'About', 'Help'],
      products : productData,
      heartCount : [0, 0, 0, 0, 0, 0],
      heartSpan : "",
      isModalOpen : false,
      choice : 0,
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
      console.log(toggle);
      this.isModalOpen = toggle;
      this.choice = index;
    }
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

.room-img {
  width:10%;
}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgb(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
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
