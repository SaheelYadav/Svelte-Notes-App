<script>
  import { createEventDispatcher } from 'svelte';

  export let note;
  const dispatch = createEventDispatcher();

  function handleConfirm() {
    dispatch('confirm');
  }

  function handleCancel() {
    dispatch('cancel');
  }
</script>

<div class="fixed inset-0 bg-black/50 backdrop-blur-sm flex items-center justify-center p-4 z-50">
  <div class="bg-white dark:bg-gray-800 rounded-xl p-8 w-full max-w-md shadow-2xl transform transition-all">
    <div class="text-center mb-6">
      <div class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-red-100 dark:bg-red-900/50 mb-4">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-red-600 dark:text-red-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
        </svg>
      </div>
      <h3 class="text-lg font-medium text-gray-900 dark:text-white mb-2">
        Delete Note
      </h3>
      <p class="text-gray-500 dark:text-gray-400">
        Are you sure you want to delete "{note.title}"? This action cannot be undone.
      </p>
    </div>

    <div class="flex justify-end space-x-4">
      <button
        on:click={handleCancel}
        class="px-6 py-2 rounded-lg border border-gray-300 dark:border-gray-600 text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors"
      >
        Cancel
      </button>
      <button
        on:click={handleConfirm}
        class="px-6 py-2 rounded-lg bg-red-500 hover:bg-red-600 text-white shadow-lg hover:shadow-xl transition-all duration-200 transform hover:-translate-y-0.5"
      >
        Delete
      </button>
    </div>
  </div>
</div> 