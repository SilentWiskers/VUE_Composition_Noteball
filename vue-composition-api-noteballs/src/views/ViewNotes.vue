<template>
    <div class="notes">

        <AddEditNote v-model="newNote" ref="addEditNoteRef" placeholder="Add a new note">
            <template v-slot:buttons>
                <button @click="addNote()" :disabled="!newNote" class="button is-link has-background-success" >Add New Note</button>
            </template>

        </AddEditNote>

        <Notes
            v-for="note in storeNotes.notes" :key="note.id" :note="note"
        />

        
    </div>
</template>

<script setup>
//Imports
import { ref } from 'vue'
import { useStoreNotes } from '@/stores/storeNotes.js'
import AddEditNote from '@/components/Notes/AddEditNote.vue'
import Notes from '@/components/Notes/NoteCard.vue'

//Notes
const storeNotes = useStoreNotes()

const newNote = ref('')
const addEditNoteRef = ref(null)


const addNote = () => {

    storeNotes.addNote(newNote.value)

    newNote.value = ''

    addEditNoteRef.value.focusTextarea()

}
 
</script>