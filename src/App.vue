<template>
          
  <add-todo
  @add="addTodo">
  </add-todo>
  <todo-block
    title="Активные задачи:" 
    middle="Активных задач нет. Добавьте новые!" 
    footer="Активных задач:"
    :notes="uncheckedTodo" 
    @remove="removeTodo">
  </todo-block>
  <todo-block
    title="Пройденные задачи:" 
    middle="Выполненных задач пока что нет!" 
    footer="Выполненных задач:"
    :notes="checkedTodo"
    @remove="removeTodo">
  </todo-block>
  <todo-modal></todo-modal>
  
</template>

<script>
import TodoBlock from '@/components/TodoBlock.vue'
import AddTodo from '@/components/AddTodo.vue'
import TodoModal from '@/components/TodoModal.vue'

export default {
  components: {
    TodoBlock, AddTodo, TodoModal
  },
  data() {
      return {
          notes: [
              // { title: 'Повторить JS', date: new Date().toLocaleString(), done: false, isEditing: false},
              // { title: 'Учить Vue', date: new Date().toLocaleString(), done: false, isEditing: false}
          ]
      }
  },
  created() {
      const todoDB = JSON.parse(localStorage.getItem('todoDB'));
      if (todoDB) {
          new Date(this.notes.date);
          this.notes = todoDB;
      }
  },
  watch: {
      notes: {
          handler() {
              localStorage.setItem('todoDB', JSON.stringify(this.notes));
          },
          deep: true
      }
  },
  methods: {
    nextId () {
        return (this.notes[this.notes.length - 1]) ? this.notes[this.notes.length - 1].id + 1 : 1
    },
    addTodo(inputValue) {
        if (inputValue !== '') {
            this.notes.push({title: inputValue, date: new Date().toLocaleString(), done: false, isEditing: false, id: this.nextId()});
        }
    },
    removeTodo(note) {
        this.notes.splice(this.notes.findIndex((el) => el.id == note.id) , 1);
    }
  },
  computed: {
    checkedTodo () {
      return this.notes.filter((el) => el.done)
    },
    uncheckedTodo () {
      return this.notes.filter((el) => !el.done)
    }
  }
}
</script>

<style>

:root {
    --bs-body-bg: #7d84b2;
}


input {
    outline: none;
}

ul {
    padding-left: 0;
}

.list_title {
    font-family: 'Oswald', sans-serif;
    color:rgb(0, 0, 0);
    justify-content: center;
}

.mcard {
    padding: 1rem;
    margin: 1rem -0.75rem 0;
    margin-left: auto;
    margin-right: auto;
    border-radius: 15px;
    border-width: 2px 2px 2px 2px;
    background-color: #a3b1de;
    max-width: 1000px;
    justify-content: center;
}

.minput_container {
    justify-content: center;
    position: relative;
    display: flex;
    flex-wrap: wrap;
    align-items: stretch;
    width: 100%;
    flex-wrap: nowrap!important;
}

.minput {
    display: block;
    width: 30%;
    padding: 0.375rem 0.75rem;
    border-radius: 10px !important;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    border-radius: 0.25rem;
}

.minput_btn {
    display: flex;
    align-items: center;
    margin-left: 5px;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    text-align: center;
    white-space: nowrap;
    background-color: #d7d7e9;
    border: 1px solid #aab0b5;
    border-radius: 0.25rem;
}

.minput_btn:hover {

}

.minput_btn:active {
    background-color:#cfd2f2;
}

.mtodo_block {
    font-family: 'Oswald', sans-serif;
    background-color: #ffffff;
    margin: 20px 20px 20px 20px;
    height: auto;
    padding: 1rem;
    margin: 1rem -0.75rem 0;
    margin-left: auto;
    margin-right: auto;
    border-radius: 15px;
    border-width: 2px 2px 2px 2px;
    max-width: 1000px;
    justify-content: space-between;
}

.grid {
    display: grid;
    grid-template-columns: 3fr 1fr 1fr;
}
.grid > div {
    padding: 0;
}

.mtodo_li {
    margin-bottom: 10px;
    list-style: none;
    border-bottom: solid 1px;
}

.mli_button {
    background: none;
    border: 0;
}

.checkbox_padding {
    padding-left: 5px;
}

.cross_out {
    text-decoration: line-through;
}

.list_footer {
    margin-top: 30px;
}

</style>
