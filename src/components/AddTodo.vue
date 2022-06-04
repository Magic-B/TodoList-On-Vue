<template>
    <div class="mcard">
      <div class="minput_container">
          <input type="text" class="minput" placeholder="Введите задачу" 
          :value="inputValue" 
          @input="inputChange"
          @keypress.enter="addTodo">
          <button type="button" class="minput_btn" @click="addList">Добавить</button>
          <button type="button" class="minput_btn" data-bs-toggle="modal" data-bs-target="#exampleModal">
            Удалить все задачи
          </button>
      </div>
  </div>
</template>

<script>
export default {
    data() {
      return {
          editValue: '',
          inputValue: '',
      }
    },
    methods: {
        inputChange(event) {
            this.inputValue = event.target.value;
        },
        addTodo() {
            this.$emit('add', this.inputValue)
            this.inputValue = '';
        }
    }
}
</script>
