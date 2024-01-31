<template>
	<div class="flex items-center justify-center w-screen h-screen font-medium">
		<div class="flex flex-col flex-grow items-center justify-center h-full text-gray-600 dark:text-gray-200 bg-gray-100 dark:bg-gray-900">
			<div class="max-w-full p-8 bg-white dark:bg-gray-800 rounded-lg shadow-lg w-96">
				<div class="flex items-center mb-6">
					<svg class="h-8 w-8 text-indigo-500 stroke-current" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4" />
					</svg>
					<h4 class="font-semibold ml-3 text-lg dark:text-white">Frodo's Jobs</h4>
				</div>

					<BaseCheckbox v-for="todo in todos" v-model="todo.completed">
						{{ todo.text }}
					</BaseCheckbox>
					
					<button class="flex items-center w-full h-8 px-2 mt-2 text-sm font-medium rounded">
						<svg class="w-5 h-5 text-gray-400 fill-current" xmlns="http://www.w3.org/2000/svg" @click="addNewTodo" fill="none" viewBox="0 0 24 24" stroke="currentColor">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
						</svg>
						<BaseInput placeholder="add a new task" v-model="newTodo" @keyup.enter="addNewTodo" />
					</button>
				</div>
				<a class="mt-5" href="https://github.com/simoneldevig/vue-todo" title="Github repository" target="_blank">
					<svg aria-hidden="true" focusable="false" role="img" class="StyledOcticon-sc-1lhyyr-0 kDaXaG" viewBox="0 0 16 16" width="NaN" height="28px" fill="currentColor" style="display: inline-block;overflow: visible;vertical-align: text-bottom;user-select: none;"><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 01-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 010 8c0-4.42 3.58-8 8-8z"></path></svg>
				</a>
		</div>
	</div>
</template>

<script setup lang="ts">
	import { ref } from 'vue';
	import BaseCheckbox from './BaseCheckbox.vue';
	import BaseInput from './BaseInput.vue';
	import { useLocalStorage } from '@vueuse/core'

	interface Todo {
		text: string;
		completed: boolean;
	}

	const newTodo = ref('');
	const todos = ref<Todo[]>([{
		text: 'Learn Vue 3',
		completed: false,
	}, {
		text: 'Learn TypeScript',
		completed: true,
	}, {
		text: 'Learn Tailwind CSS',
		completed: true,
	}]);

	useLocalStorage(
		'todos',
		todos,
	);

	const addNewTodo = () => {
		if (newTodo.value) {
			todos.value.push({
				text: newTodo.value,
				completed: false,
			});
			newTodo.value = '';
		}
	};
</script>
