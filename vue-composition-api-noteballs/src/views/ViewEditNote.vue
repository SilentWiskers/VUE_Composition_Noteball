<template>
    <div class="edit-Note">
        <AddEditNote v-model="noteContent" ref="addEditNoteRef" bgColor="link" placeholder="Edit Note" label="Edit Note">
            <template v-slot:buttons>
                <RouterLink :to="'/'" class="button is-link is-light mr-2" >Cancel</RouterLink>
                <button @click="handleSaveClicked" :disabled="!noteContent" class="button is-link has-background-link" >Save Note</button>
            </template>

        </AddEditNote>
    </div>
</template>


<script setup>

//Imports
    import AddEditNote from '@/components/Notes/AddEditNote.vue'
    import { useStoreNotes } from '@/stores/storeNotes.js'
    import { useRoute, useRouter } from 'vue-router'
    import { ref } from 'vue'


//Router
    const route = useRoute()
    const router = useRouter()


//Variables

    const noteContent = ref('')

    const storeNotes = useStoreNotes()

    noteContent.value = storeNotes.getNoteContent(route.params.id)

//Save Note

    const handleSaveClicked = () => {
        storeNotes.updateNote(route.params.id, noteContent.value)
        router.push('/')
    }




</script>