<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <Modal :show="showModal" @close="showModal = false">
      <template #header>
        <h3 slot="header">
          경고!!!
          <i class="closeModalBtn fa fa-times" aria-hidden="true" @click="showModal = false"></i>
        </h3>
        <div slot="body"> 아무것도 입력하지 않으셨습니다. </div>
      </template>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/modal.vue'
import { mapMutations } from 'vuex';

export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        const newTodotext = this.newTodoItem.trim();
        //this.$emit('addTodoItem',this.newTodoItem);
        this.$store.commit('addOneItem', newTodotext);
        this.clearInput();
      } else{
        
        this.showModal = !this.showModal 
        
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
}
</script>

<style scoped>
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
</style>
