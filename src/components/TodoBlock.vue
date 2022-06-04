<template>
    <div class="mtodo_block">
        <h1> {{ title }} </h1>
        <ul class="mtodo_list" v-if="notes.length !== 0">
            <li class="mtodo_li" v-for="(note) in notes" :key="note.id">

                <div class="grid">
                <div>
                    <input type="text" v-if="note.isEditing" @keypress.enter="note.isEditing = false" v-model="note.title">
                    <label 
                    class="form-check-label checkbox_padding" 
                    v-else 
                    :class="{cross_out: note.done}">
                    {{ note.title }}
                </label>
                </div>
                
                <div>
                {{ note.date }}
                </div>
                
                <div>
                <button class="mli_button" @click="note.isEditing = !note.isEditing"><i class="fa-solid fa-pen"></i></button>
                <button class="mli_button" @click="$emit('remove', note)"><i class="fa-solid fa-trash-can"></i></button>
                <button class="mli_button" @click="note.done = !note.done"><i class="fa-solid fa-circle-check"></i></button>
                </div>

                </div>
            </li>
        </ul>
        <h5 class="mlist_title" v-if="notes.length == 0"> {{ middle }} </h5>
        <div class="list_footer">
            <hr>
            <div> {{ footer }} {{ notes.length }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TodoBlock',
    props: ['title', 'middle', 'footer', 'notes'],
    data() {
      return {
        
      }
    }
}
</script>