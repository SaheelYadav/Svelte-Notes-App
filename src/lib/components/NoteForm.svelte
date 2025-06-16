<script>
  import { createEventDispatcher } from 'svelte';

  export let note = null;
  const dispatch = createEventDispatcher();

  let title = note?.title || '';
  let content = note?.content || '';

  function handleSubmit() {
    if (!title.trim() || !content.trim()) return;

    dispatch('submit', {
      id: note?.id,
      title: title.trim(),
      content: content.trim(),
      createdAt: note?.createdAt || new Date().toISOString()
    });

    title = '';
    content = '';
  }

  function handleCancel() {
    dispatch('cancel');
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="space-y-6">
  <div>
    <label for="title" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
      Title
    </label>
    <input
      type="text"
      id="title"
      bind:value={title}
      class="w-full px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-colors"
      placeholder="Enter note title"
      required
    />
  </div>

  <div>
    <label for="content" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
      Content
    </label>
    <textarea
      id="content"
      bind:value={content}
      rows="6"
      class="w-full px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-colors resize-none"
      placeholder="Enter note content"
      required
    ></textarea>
  </div>

  <div class="flex justify-end space-x-4">
    <button
      type="button"
      on:click={handleCancel}
      class="px-6 py-2 rounded-lg border border-gray-300 dark:border-gray-600 text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors"
    >
      Cancel
    </button>
    <button
      type="submit"
      class="px-6 py-2 rounded-lg bg-gradient-to-r from-blue-500 to-purple-500 hover:from-blue-600 hover:to-purple-600 text-white shadow-lg hover:shadow-xl transition-all duration-200 transform hover:-translate-y-0.5"
    >
      {note ? 'Update Note' : 'Create Note'}
    </button>
  </div>
</form> 