<template>
  <div class="modal open">
      <div class="modal-box">
        <div class="modal-name-box">nickname: <input type="text" v-model="updateData.nickname"></div>
        <div class="modal-img-box"><img style="object-fit: cover;" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTJ6yI5v-1UCyMx8CdTpABg9QzItPHcPLZh7_1ZnzOpTg&s" alt=""></div>
        <div @click="toggleModal" class="modal-x-button"><i class="fa-solid fa-xmark"></i></div>
        <div class="modal-follow-box">
          <div></div>
          <div></div>
        </div>
        <div class="detail-deco-bar"></div>
        <div class="trainer-detail-info-box">
          <div class="split-box-info1">
            <div class="modal-info">나이: <input type="number" v-model="updateData.age"> 성별:<input type="number" v-model="updateData.gender"> </div>
            <div class="modal-info">
              신장 <input type="number" v-model="updateData.height">
              무게: <input type="number" v-model="updateData.user_weight">
              목표 무게: <input type="number" v-model="updateData.object_weight">
            </div>
            <div class="modal-info">트레이닝 비용: <input type="number" v-model="updateData.exercise_price"></div>
            <div class="modal-info">코멘트: <input type="text" v-model="updateData.comment"></div>
          </div>
          <div class="split-box-info2">
            <div class="modal-info">경력: <input type="text" v-model="updateData.career"></div>
            <div class="modal-info">식단관리 비용: <input type="number" v-model="updateData.diet_price"></div>
          </div>
        </div>
        <div class="modal-view-button">
          <div></div>
          <button type="button" class="trainer-apply-style" @click="onClick">신청하기</button>
          <div></div>
        </div>
      </div>
    </div>
</template>

<script>
import { reactive } from '@vue/reactivity'
import { useStore } from 'vuex'
export default {
  setup () {
    const store = useStore()
    const getUpdate = store.dispatch('updateTrainer')
    const updateData = reactive({
      age: null,
      gender: null,
      height: null,
      user_weight: null,
      object_weight: null,
      exercise_category: null,
      career: null,
      diet_price: null,
      exercise_price: null,
      comment: null
    })
    function onClick () {
      store.dispatch('updateTrainer', updateData)
    }
    return {
      store,
      getUpdate,
      updateData,
      onClick
    }
  }
}
</script>

<style scope>
.modal {
  min-height: 315px;
  font-size: 16px;
  font-family: 'MaruBuriOTF';
  font-style: normal;
  position: fixed;
  display: none;
  z-index: 200;
  top: 20%;
  left: 30%;
  width: 40%;
  height: 60%;
  background: white;
  border: 1px solid #6dcef5;
  border-radius: 15px;
  box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.5);
}
.modal-box {

  margin: 5%;
  width: 90%;
  height: 90%;
}
.modal-name-box {
  text-align: center;
}
.modal-img-box {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 40%;
}
.modal-follow-box {
  display: flex;
  justify-content: space-around;
}
.open {
  display: block !important;
}
.modal-x-button {
  position: absolute;
  top: 3%;
  left: 95%;
}
.detail-deco-bar {
  position: relative;
  margin: 0px 15% 0px 15%;
  width: calc(70% - 6px);
  height: 0px;
  border: 1px solid #000000;
}
.trainer-detail-info-box {
  display: flex;
  margin: 0px 15% 0px 15%;
  width: 70%;
  height: 35%;
}
.split-box-info1 {
  display: inline;
  width: 50%;
}
.split-box-info2 {
  display: inline;
  width: 50%;
}
.modal-view-button {
  display: flex;
  justify-content: space-around;
  margin: auto;
}
.modal-info {
  padding: 4%;
}
.trainer-apply-style {
  box-sizing: border-box;
  width: 100px;
  height: 30px;
  font-size: 16px;
  font-family: 'MaruBuriOTF';
  font-style: normal;
  padding: 5px 15px;
  border: 1px solid #6dcef5;
  gap: 10px;
  border-radius: 25px;
  background-color: #FFF;
  color: #6dcef5;
  text-decoration-line: none;
  text-align: center;
}
</style>
