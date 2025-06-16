<script>
  import { createEventDispatcher } from 'svelte';

  export let note;
  const dispatch = createEventDispatcher();

  function formatDate(dateString) {
    const date = new Date(dateString);
    return new Intl.DateTimeFormat('en-US', {
      year: 'numeric',
      month: 'short',
      day: 'numeric',
      hour: '2-digit',
      minute: '2-digit'
    }).format(date);
  }
</script>

<div class="group bg-white dark:bg-gray-800 rounded-xl shadow-lg hover:shadow-2xl transition-all duration-300 overflow-hidden border border-gray-100 dark:border-gray-700 hover:border-blue-200 dark:hover:border-blue-800 relative">
  <div class="absolute inset-0 bg-gradient-to-br from-blue-50 to-purple-50 dark:from-blue-900/10 dark:to-purple-900/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
  
  <div class="p-6 relative">
    <div class="flex justify-between items-start mb-3">
      <h3 class="text-xl font-semibold text-gray-900 dark:text-white line-clamp-2 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors duration-300">
        {note.title}
      </h3>
      <div class="flex space-x-2">
        <button
          on:click={() => dispatch('edit', note)}
          class="p-2 text-gray-500 hover:text-blue-500 dark:text-gray-400 dark:hover:text-blue-400 transition-all duration-200 rounded-lg hover:bg-blue-50 dark:hover:bg-blue-900/30 transform hover:scale-110"
          title="Edit note"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
            <path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z" />
          </svg>
        </button>
        <button
          on:click={() => dispatch('delete', note)}
          class="p-2 text-gray-500 hover:text-red-500 dark:text-gray-400 dark:hover:text-red-400 transition-all duration-200 rounded-lg hover:bg-red-50 dark:hover:bg-red-900/30 transform hover:scale-110"
          title="Delete note"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
          </svg>
        </button>
      </div>
    </div>
    
    <div class="relative">
      <div class="prose dark:prose-invert max-w-none">
        <p class="text-[15px] text-gray-700 dark:text-gray-200 line-clamp-4 mb-3 group-hover:text-gray-800 dark:group-hover:text-gray-100 transition-colors duration-300 leading-7 tracking-wide">
          {note.content}
        </p>
      </div>
    </div>

    <div class="mt-3 pt-3 border-t border-gray-100 dark:border-gray-700">
      <div class="flex items-center text-sm text-gray-500 dark:text-gray-400 group-hover:text-gray-600 dark:group-hover:text-gray-300 transition-colors duration-300">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1.5" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z" clip-rule="evenodd" />
        </svg>
        <span class="font-medium">{formatDate(note.createdAt)}</span>
      </div>
    </div>
  </div>
</div> 