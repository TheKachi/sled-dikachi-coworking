<template>
	<div id="app" class="w-screen h-screen overflow-hidden">
		<!-- Column Selector Container -->
		<div
			class="mx-auto mt-[100px] px-[200px] flex gap-[40px] md:gap-[60px] items-start"
		>
			<div>
				<p class="text-[#475569] text-[14px] mb-[6px]">Columns</p>

				<ColumnSelector
					:columns="unselectedColumns"
					:selected="selectedColumns"
					:filtered="filteredColumns"
					@toggle="toggleColumn"
					@remove="removeColumn"
					@clear-search="clearSearch"
					v-model="query"
				/>
			</div>

			<!-- Show Dialog button  -->
			<button
				id="show-modal"
				@click="showDialog = true"
				class="border px-[24px] py-[4px] mt-[24px]"
			>
				Show Modal
			</button>
		</div>

		<Modal :isActive="showDialog" @close="showDialog = false">
			<div slot="header">
				<div class="flex flex-col gap-[4px] items-start">
					<div class="flex gap-[4px] items-center">
						<img
							src="./assets/icons/gear.svg"
							alt="settings icon"
							class="w-[24px] h-[24px]"
						/>
						<h5 class="text-lg lg:text-2xl font-bold text-black">
							Checks
						</h5>
					</div>

					<p class="text-[#868686] text-[16px]">
						Check help to control the data expected and fulfills a defined
						service level. Activated checks are executed on a schedule.
					</p>
				</div>
			</div>

			<div slot="body">
				<div
					class="md:max-h-[400px] overflow-y-scroll flex flex-col gap-[6px]"
				>
					<p class="text-[#475569] text-[14px]">Columns</p>
					<div>
						<ul v-if="filteredColumns.length > 0" class="bg-white h-full">
							<li
								v-for="column in filteredColumns"
								:key="column"
								class="px-[10px] py-[6px] text-[#475569] text-[13px] hover:bg-[#F5F5F5] cursor-pointer"
							>
								{{ column }}
							</li>
						</ul>
					</div>
					<!-- 
					<ColumnSelector
						:columns="columns"
						:selected-columns="selectedColumns"
						:filtered-columns="filteredColumns"
						@add="addColumn"
						@remove="removeColumn"
					/> -->
					<!-- v-model="query" -->
				</div>
			</div>

			<div slot="footer">
				<div class="flex justify-end gap-[8px]">
					<button
						class="border px-[24px] py-[4px] mt-[24px]"
						@click="showDialog = false"
					>
						Cancel
					</button>

					<button
						class="bg-black text-white px-[24px] py-[4px] mt-[24px]"
						@click="showDialog = false"
					>
						Save
					</button>
				</div>
			</div>
		</Modal>
	</div>
</template>

<script>
import ColumnSelector from "./components/ColumnSelector.vue";
import Modal from "./components/Modal.vue";

export default {
	name: "App",

	data() {
		return {
			columns: [
				"ID",
				"Total",
				"Links",
				"Number",
				"Status",
				"Billing",
				"Refunds",
				"Version",
				"Cart_Tax",
				"Currency",
				"Set_Paid",
				"Shipping",
				"Cart_Hash",
				"Date_Paid",
				"Fee_Lines",
			],
			selectedColumns: [],
			unselectedColumns: [],
			query: "",
			anotherQuery: "",
			isShowing: false,
			showDialog: false,
		};
	},

	methods: {
		toggleDropdown() {
			this.isShowing = !this.isShowing;
		},

		// add column to selectedColumns array
		toggleColumn(column) {
			// remove from selected array
			if (this.selectedColumns.includes(column)) {
				this.removeColumn(column);
			} else {
				this.addColumn(column);
			}
		},

		// add column to selectedColumns array and move to the top
		addColumn(column) {
			this.selectedColumns.push(column);
			this.unselectedColumns = this.unselectedColumns.filter(
				(c) => c !== column
			);

			this.clearSearch();
			// // move column to the top
		},

		// remove column from selectedColumns array and move to the bottom
		removeColumn(column) {
			this.selectedColumns = this.selectedColumns.filter(
				(c) => c !== column
			);

			//  unselected array
			this.unselectedColumns.unshift(column);

			this.clearSearch();
		},

		clearSearch() {
			this.query = "";
		},
	},

	filterColumns(columns) {
		if (this.query !== "") {
			return columns.filter((column) =>
				column.toLowerCase().includes(this.query.toLowerCase())
			);
		} else return columns;
	},

	computed: {
		// return the column that matches the search query
		filteredColumns() {
			let columns = this.selectedColumns.concat(this.unselectedColumns);
			if (this.query !== "") {
				return columns.filter((column) =>
					column.toLowerCase().includes(this.query.toLowerCase())
				);
			} else return columns;
		},
	},
	components: {
		// Dialog,
		Modal,
		ColumnSelector,
	},
	mounted() {
		this.unselectedColumns = this.columns;
	},
};
</script>

<style></style>
