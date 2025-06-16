<script>
  import { onMount } from 'svelte';
  import axios from 'axios';
  import NoteList from './lib/components/NoteList.svelte';
  import NoteForm from './lib/components/NoteForm.svelte';
  import DeleteConfirmation from './lib/components/DeleteConfirmation.svelte';

  let notes = [];
  let loading = true;
  let error = null;
  let showDeleteModal = false;
  let noteToDelete = null;
  let showForm = false;
  let editingNote = null;

  const API_URL = 'https://684fb25de7c42cfd17958730.mockapi.io/api/notes';

  async function fetchNotes() {
    try {
      loading = true;
      const response = await axios.get(API_URL);
      notes = response.data;
      error = null;
    } catch (e) {
      error = e.message;
    } finally {
      loading = false;
    }
  }

  async function handleCreateNote(event) {
    const note = event.detail;
    try {
      const response = await axios.post(API_URL, {
        title: note.title,
        content: note.content,
        createdAt: new Date().toISOString()
      });
      notes = [response.data, ...notes];
      showForm = false;
    } catch (e) {
      error = e.message;
    }
  }

  async function handleUpdateNote(event) {
    const note = event.detail;
    if (!note?.id) {
      error = 'Invalid note ID';
      return;
    }

    try {
      const response = await axios.put(`${API_URL}/${note.id}`, {
        title: note.title,
        content: note.content,
        createdAt: note.createdAt
      });
      
      if (response.data) {
        notes = notes.map(n => n.id === response.data.id ? response.data : n);
        editingNote = null;
        showForm = false;
      }
    } catch (e) {
      error = e.message;
    }
  }

  async function handleDeleteNote(id) {
    if (!id) {
      error = 'Invalid note ID';
      return;
    }
    
    try {
      const response = await axios.delete(`${API_URL}/${id}`);
      if (response.status === 200) {
        notes = notes.filter(note => note.id !== id);
        showDeleteModal = false;
        noteToDelete = null;
      }
    } catch (e) {
      error = e.message;
    }
  }

  function openDeleteModal(event) {
    const note = event.detail;
    if (!note?.id) {
      error = 'Invalid note';
      return;
    }
    noteToDelete = note;
    showDeleteModal = true;
  }

  function openEditForm(event) {
    const note = event.detail;
    if (!note?.id) {
      error = 'Invalid note';
      return;
    }
    editingNote = note;
    showForm = true;
  }

  onMount(fetchNotes);
</script>

<main class="min-h-screen bg-gradient-to-br from-gray-100 via-gray-50 to-gray-200 dark:from-gray-800 dark:via-gray-900 dark:to-gray-950">
  <div class="container mx-auto px-4 py-12">
    <header class="mb-12 text-center">
      <h1 class="text-5xl font-bold text-gray-900 dark:text-white mb-4 bg-clip-text text-transparent bg-gradient-to-r from-blue-500 to-purple-500">
        Notes App
      </h1>
      <p class="text-lg text-gray-600 dark:text-gray-400">
        Keep your thoughts organized and accessible
      </p>
    </header>

    {#if error}
      <div class="max-w-2xl mx-auto mb-8 bg-red-50 dark:bg-red-900/50 border border-red-200 dark:border-red-800 text-red-700 dark:text-red-200 px-6 py-4 rounded-lg shadow-sm" role="alert">
        <p class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
          </svg>
          {error}
        </p>
      </div>
    {/if}

    <div class="max-w-2xl mx-auto mb-12">
      <button
        on:click={() => { showForm = true; editingNote = null; }}
        class="w-full bg-gradient-to-r from-blue-500 to-purple-500 hover:from-blue-600 hover:to-purple-600 text-white px-6 py-3 rounded-lg shadow-lg hover:shadow-xl transition-all duration-200 transform hover:-translate-y-0.5 flex items-center justify-center space-x-2"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
        </svg>
        <span>Create New Note</span>
      </button>
    </div>

    {#if showForm}
      <div class="fixed inset-0 bg-black/50 backdrop-blur-sm flex items-center justify-center p-4 z-50">
        <div class="bg-white dark:bg-gray-800 rounded-xl p-8 w-full max-w-lg shadow-2xl transform transition-all">
          <NoteForm
            note={editingNote}
            on:submit={editingNote ? handleUpdateNote : handleCreateNote}
            on:cancel={() => { showForm = false; editingNote = null; }}
          />
        </div>
      </div>
    {/if}

    {#if showDeleteModal && noteToDelete}
      <DeleteConfirmation
        note={noteToDelete}
        on:confirm={() => handleDeleteNote(noteToDelete.id)}
        on:cancel={() => { showDeleteModal = false; noteToDelete = null; }}
      />
    {/if}

    {#if loading}
      <div class="flex justify-center items-center h-64">
        <div class="animate-spin rounded-full h-12 w-12 border-4 border-blue-500 border-t-transparent"></div>
      </div>
    {:else}
      <div class="max-w-6xl mx-auto">
        <NoteList
          {notes}
          on:edit={openEditForm}
          on:delete={openDeleteModal}
        />
      </div>
    {/if}
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
</style>
