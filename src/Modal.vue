<template>
  <div class="black-bg" v-if="isModalOpen === true">
    <div class="white-bg">
      <h4>{{ products[choice].title }}</h4>
      <img :src=products[choice].image  alt="" />
      <p>{{ products[choice].content }}</p>
      <!-- 아래 문법과 비슷함 <input @input="pcs = $event.target.value">-->
      <input v-model.number="pcs">
      <p>{{ pcs }}개 선택함 : {{ products[choice].price * pcs }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Modal",
  data() {
    return {
      pcs : 1,
    }
  },
  watch : {
    pcs(val) {
      //문자를 입력시 경고창 띄우기 + 초기값으로 되돌리기
      //vue 전용 form-validation 라이브러리 지원함.
      console.log(typeof(val));
      if(typeof(val) != 'number') {
        alert("숫자만 입력가능합니다.");
        this.pcs = 1;
      }
    }
  },
  props : {
    products : Array,
    choice : Number,
    isModalOpen : Boolean,
  },
}
</script>

<style scoped>
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