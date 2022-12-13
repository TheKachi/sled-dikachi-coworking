<template>
	<div>
		<!-- Change to reg div w aria label -->
		<div @click="toggleDropdown" class="relative">
			<input
				type="search"
				:value="query"
				v-on:input="$emit('search', $event.target.value)"
				aria-label="search"
				placeholder="Search or select"
			/>
			<!-- <ul v-if="selectedColumns.length > 0">
				<li v-for="column in selectedColumns" :key="column">
					<button @click="$emit(remove(column))">X</button>
					{{ column }}
				</li>
			</ul> -->
		</div>

		<ul v-if="showDropdown" class="absolute w-full">
			<!-- @click="$emit(add(column))" -->
			<li v-for="column in columns" :key="column">
				<!-- <input
					type="checkbox"
					:value="column"
					v-on:input="$emit('input', $event.target.value)"
					@change="$emit('add', $event.target.value)"
				/> -->
				<!-- <input
					type="checkbox"
					:value="column"
					v-bind:checked="checked"
					v-on:change="$emit('change', $event.target.checked)"
				/> -->
				<input
					type="checkbox"
					:id="column"
					:value="column"
					:name="column"
					:checked="selectedColumns.includes(column)"
					v-on:change="$emit('add', $event.target.value)"
				/>
				{{ column }}
			</li>
		</ul>

		<div>
			<h4>Selected Columns:</h4>
			{{ selectedColumns }}
			<ul v-for="column in selectedColumns" :key="column">
				<li>
					<button @click="$emit('remove')">X</button>
					{{ column }}
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	name: "App",

	model: {
		prop: "checked",
		event: "change",
	},

	props: {
		checked: Boolean,
		cmd: {
			type: String,
			default: "Select Columns",
		},
		value: {
			type: String,
			default: "",
		},
		columns: {
			type: Array,
			default: () => [],
		},
		selectedColumns: {
			type: Array,
			default: () => [],
		},
	},

	emits: ["search", "input", "add", "remove"],

	data() {
		return {
			showDropdown: false,
		};
	},

	methods: {
		toggleDropdown() {
			this.showDropdown = !this.showDropdown;
		},
	},

	// methods: {
	// 	// add column to selectedColumns array
	// 	addColumn(column) {
	// 		this.selectedColumns.push(column);
	// 	},
	// 	// remove column from selectedColumns array
	// 	removeColumn(column) {
	// 		this.selectedColumns = this.selectedColumns.filter(
	// 			(c) => c !== column
	// 		);
	// 	},
	// },

	// computed: {
	// 	// return the column that matches the search query
	// 	columns() {
	// 		return this.columns.filter((column) =>
	// 			column.toLowerCase().includes(this.query.toLowerCase())
	// 		);
	// 	},
	// },
};
</script>

<style></style>
