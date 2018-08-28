<template lang="html">
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">
        할 일을 입력하세요.
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false // 모달 동작을 위한 플래그 값
    }
  },
  methods: {
    addTodo() {
      if(this.newTodoItem !== ""){ // 입력 값 있을 때만 저장
        var value = this.newTodoItem && this.newTodoItem.trim(); // 앞 뒤 공백 제거
        this.$emit('addTodo', value);
        this.clearInput();
      } else {
        this.showModal = !this.showModal; // 텍스트 미입력 시 모달 동작
      }
    },
    clearInput() { // 입력 값 초기화
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal
  }
}
</script>

<style lang="css" scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
  /* 모달 */
  .modal-header h3, .modal-footer i {
    margin-top: 0;
    color: #42b983;
  }

</style>
