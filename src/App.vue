<template>
	<div id="app">
		<div>
			<div @click="toggleDropdown" class="border w-[250px]">
				<input
					class="w-full"
					type="text"
					v-model="query"
					placeholder="Search or select a column"
				/>
			</div>

			<ul v-if="isShowing">
				<li
					@click.prevent="addColumn(column)"
					v-for="column in filteredColumns"
					:key="column"
				>
					<input
						type="checkbox"
						:value="column"
						v-model="selectedColumns"
					/>
					{{ column }}
				</li>
			</ul>
			<div v-if="selectedColumns.length > 0">
				<ul v-for="column in selectedColumns" :key="column">
					<li>
						<button @click="removeColumn(column)">X</button>
						{{ column }}
					</li>
				</ul>
			</div>
		</div>
		<!-- <ColumnSelector
			:columns="columns"
			:selected-columns="selectedColumns"
			@search="query = $event"
			@add="addColumn"
			@remove="removeColumn"
		/> -->
	</div>
</template>

<script>
// import ColumnSelector from "./components/ColumnSelector.vue";

export default {
	name: "App",
	data() {
		return {
			columns: ["ID", "Total", "Links", "Number", "Status"],
			selectedColumns: [],
			query: "",
			isShowing: false,
		};
	},
	methods: {
		toggleDropdown() {
			this.isShowing = true;
		},
		// add column to selectedColumns array
		addColumn(column) {
			if (this.selectedColumns.includes(column)) return;
			this.selectedColumns.push(column);
			// this.isShowing = false;
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
		// orderedSelectedColumns() {
		// 	return this.selectedColumns.sort();
		// },
	},
	// components: { ColumnSelector },
};
</script>

<style></style>
