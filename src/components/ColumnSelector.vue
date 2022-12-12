<!-- v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)" -->

<template>
	<div id="app">
		<div>
			<!-- Change to reg div w aria label -->
			<input
				type="text"
				v-model="query"
				placeholder="Search for columns..."
			/>
			<!-- Hide and show with aria labels -->
			<ul>
				<li v-for="column in columns" :key="column">
					<input
						type="checkbox"
						:value="column"
						v-model="selectedColumns"
						@change="addColumn(column)"
					/>
					{{ column }}
				</li>
			</ul>
			<div v-if="selectedColumns.length > 0">
				<h4>Selected Columns:</h4>
				{{ selectedColumns }}}
				<ul v-for="column in selectedColumns" :key="column">
					<li>
						<button @click="removeColumn(column)">X</button>
						{{ column }}
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "App",

	data() {
		return {
			// The available columns for selection
			columns: ["ID", "Total", "Links", "Number", "Status"],

			// The selected columns
			selectedColumns: [],
			// The search query
			query: "",
		};
	},

	methods: {
		// add column to selectedColumns array
		addColumn(column) {
			this.selectedColumns.push(column);
		},
		// remove column from selectedColumns array
		removeColumn(column) {
			this.selectedColumns = this.selectedColumns.filter(
				(c) => c !== column
			);
		},
	},

	computed: {
		// return the column that matches the search query
		filteredColumns() {
			return this.columns.filter((column) =>
				column.toLowerCase().includes(this.query.toLowerCase())
			);
		},
	},
};
</script>

<style></style>
