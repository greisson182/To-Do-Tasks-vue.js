<template>
	<div id="app">
		<TaskProgress :progress="progress"/>
		<h1>To do Tasks</h1>
		<NewTask @taskAdded="addTask" />
		<TaskGrid 
			:tasks="tasks"
			@taskDeleted="deleteTask"
			@togleTaksState="togleTaksState"
		/>
	</div>
</template>

<script>

import NewTask from './components/NewTask.vue';
import TaskGrid from './components/TaskGrid.vue';
import TaskProgress from './components/TaskProgress.vue';

export default {
	components: { TaskGrid, NewTask, TaskProgress },
	data() {
		return {
			tasks: []
		}
	}, 
	computed: {
		progress() {
			const amount = this.tasks.length;
			const done = this.tasks.filter(t => !t.pending).length

			return Math.round(done / amount * 100) || 0
		}
	},
	watch: {
		tasks: {
			deep: true,
			handler() {
				localStorage.setItem('tasks', JSON.stringify(this.tasks));	
			}
		}
	},
	methods: {
		addTask(task) {
			const sameName = t => t.name === task.name;
			const reallyNew = this.tasks.filter(sameName).length == 0
				
			if (reallyNew && task.name != '') {
				this.tasks.push({
					name: task.name,
					pending: task.pending || true,
				});
			}
		},
		deleteTask(i) {
			this.tasks.splice(i, 1);
		},
		togleTaksState(i) {
			this.tasks[i].pending = !this.tasks[i].pending;
		}
	},
	created() {
		const json = localStorage.getItem('tasks');
		this.tasks = JSON.parse(json) || [];
	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
