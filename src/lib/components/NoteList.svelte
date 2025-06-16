<script>
  import { createEventDispatcher } from 'svelte';
  import NoteCard from './NoteCard.svelte';

  export let notes = [];
  const dispatch = createEventDispatcher();

  function handleEdit(note) {
    dispatch('edit', note);
  }

  function handleDelete(note) {
    dispatch('delete', note);
  }
</script>

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {#each notes as note (note.id)}
    <div class="transform transition-all duration-300 hover:-translate-y-1">
      <NoteCard
        {note}
        on:edit={() => handleEdit(note)}
        on:delete={() => handleDelete(note)}
      />
    </div>
  {/each}
</div>

{#if notes.length === 0}
  <div class="text-center py-12">
    <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-gray-100 dark:bg-gray-800 mb-4">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
      </svg>
    </div>
    <h3 class="text-lg font-medium text-gray-900 dark:text-white mb-2">No notes yet</h3>
    <p class="text-gray-500 dark:text-gray-400">Create your first note to get started!</p>
  </div>
{/if} 