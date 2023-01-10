<template>
<!--  <div v-for="(product,i) in products" :key='i'>
    <h4>{{product.title}}</h4>
    <img @click="ModalOpen(true, i);" class="room-img" :src=product.image alt="" />
    <p>{{product.price}}원</p>
    <p>좋아요 수 : {{heartCount[i]}}</p>
    <button @click="heartAdd(i);">좋아요</button>
  </div>-->

  <div>
    <h4>{{product.title}}</h4>
    <img @click="$emit('openModal', product.id)" class="room-img" :src=product.image alt="" />
    <p>{{product.price}}원</p>
    <p>좋아요 수 : {{ heartCount }}</p>
    <button @click="$emit('heartAdd', product.id);">좋아요</button>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Card",
  props: {
    product : Object,
    index : Number,
    heartCount : Number
  },
}
</script>

<style scoped>
.room-img {
  width:10%;
}
</style>