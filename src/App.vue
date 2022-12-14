<template>
	<div id="app" class="w-screen overflow-hidden">
		<!-- Column Selector Container -->
		<div
			class="mx-auto mt-[100px] px-[200px] flex gap-[40px] md:gap-[60px] items-start"
		>
			<div>
				<p class="text-[#475569] text-[14px] mb-[6px]">Columns</p>
				<ColumnSelector
					:columns="columns"
					:selected-columns="selectedColumns"
					:filtered-columns="filteredColumns"
					v-model="query"
					@search="query = $event"
					@add="addColumn"
					@remove="removeColumn"
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

		<Modal v-if="showDialog" @close="showDialog = false">
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
				<div class="md:min-h-[400px] flex flex-col gap-[6px]">
					<p class="text-[#475569] text-[14px]">Columns</p>

					<ColumnSelector
						:columns="columns"
						:selected-columns="selectedColumns"
						:filtered-columns="filteredColumns"
						v-model="query"
						@add="addColumn"
						@remove="removeColumn"
					/>
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
						class="bg-[#2F80ED] text-white px-[24px] py-[4px] mt-[24px]"
						@click="showDialog = false"
					>
						Save
					</button>
				</div>
			</div>
		</Modal>

		<!-- Dialog  -->
		<!-- <Dialog v-if="showDialog" @close="showDialog = false">
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
				<div class="flex flex-col gap-[6px]">
					<p class="text-[#475569] text-[14px]">Columns</p>

					<ColumnSelector
						:columns="columns"
						:selected-columns="selectedColumns"
						:filtered-columns="filteredColumns"
						v-model="query"
						@add="addColumn"
						@remove="removeColumn"
					/>
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
						class="bg-[#2F80ED] text-white px-[24px] py-[4px] mt-[24px]"
						@click="showDialog = false"
					>
						Save
					</button>
				</div>
			</div>
		</Dialog> -->
	</div>
</template>

<script>
// import ColumnSelector from "./components/ColumnSelector.vue";
import ColumnSelector from "./components/ColumnSelector.vue";
import Modal from "./components/Modal.vue";
// import Dialog from "./components/Dialog.vue";

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
			query: "",
			isShowing: false,
			showDialog: false,
		};
	},
	methods: {
		// showDropdown() {
		// 	this.isShowing = true;
		// },

		// closeDropdown() {
		// 	toggleDropdown();
		// 	alert(this.isShowing);
		// },

		toggleDropdown() {
			this.isShowing = !this.isShowing;
		},

		// add column to selectedColumns array
		addColumn(column) {
			if (this.selectedColumns.includes(column)) return;
			this.selectedColumns.unshift(column);
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
	components: {
		// Dialog,
		Modal,
		ColumnSelector,
	},
};
</script>

<style></style>
