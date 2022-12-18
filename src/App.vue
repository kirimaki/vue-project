<template>
  <div class="black-bg" v-if="isModalOpen == true">
    <div class="white-bg">
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
      <button @click="ModalOpen(false);">닫기</button>
    </div>
  </div>
  
  <div class="menu">
    <a v-for="(menuName,i) in menu" :key='i'>{{menuName}}</a>
  </div>

  <div v-for="(product,i) in products" :key='i'>
    <h4>{{product.title}}</h4>
    <!--<img class="room-img" src="./assets/"+{{image[i]}}+".png">-->
    <img @click="ModalOpen(true);" class="room-img" :src=product.image>
    <p>{{product.price}}원</p>
    <p>좋아요 수 : {{heartCount[i]}}</p>
    <button @click="heartAdd(i);">좋아요</button>
  </div>
  <button v-on:click="heartShot();">하트뿅뿅</button>
  <span id="heart">{{heartSpan}}</span>
</template>

<script>

import productData from './assets/product.js';

export default {
  name: 'App',
  data() {
    return {
      menu : ['Home', 'Products', 'About', 'Help'],
      products : productData,
      heartCount : [0, 0, 0],
      heartSpan : "",
      isModalOpen : false,
    }
  },
  methods : {
    heartAdd(index) {
      this.heartCount[index] += 1;
    },
    heartShot() {
      this.heartSpan += "♥";
    },
    ModalOpen(toggle) {
      this.isModalOpen = toggle;
    }
  },
  components: {
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

.room-image {
  width:100%;
  margin-top : 40px;
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
</style>
