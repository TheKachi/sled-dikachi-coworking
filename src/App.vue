<template>
	<div id="app">
		<div class="mx-auto mt-[50px] px-[200px] flex gap-[20px] items-start">
			<!-- Column Selector Container -->
			<div class="w-[400px] relative">
				<!-- Select Dropdown -->
				<div
					@click="isShowing = true"
					class="text-[14px] px-[10px] py-[10px] flex items-center cursor-pointer rounded-4 z-0 bg-[#F8FAFC] focus:bg-[#F8FAFC]"
				>
					<div class="relative w-full">
						<!-- Selected columns in order -->
						<ul
							class="flex flex-wrap gap-[4px]"
							v-if="selectedColumns.length"
						>
							<li
								v-for="column in selectedColumns"
								:key="column"
								class="border flex items-center justify-between rounded text-center p-[4px] text-xs text-[#475569] bg-[#F8FAFC] border-[#E2E8F0]"
							>
								{{ column }}
								<button @click="removeColumn(column)">
									<svg
										width="10"
										height="10"
										viewBox="0 0 16 16"
										fill="none"
										xmlns="http://www.w3.org/2000/svg"
									>
										<path
											d="M12 4L4 12"
											stroke="#475569"
											stroke-linecap="round"
											stroke-linejoin="round"
										/>
										<path
											d="M4 4L12 12"
											stroke="#475569"
											stroke-linecap="round"
											stroke-linejoin="round"
										/>
									</svg>
								</button>
							</li>
						</ul>

						<!-- No column selected  -->
						<p class="text-[#475569] text-14" v-else>
							Search or select a dropdown
						</p>

						<!-- Show and Hide icons  -->
						<div class="absolute z-40 -right-[8px] top-[4px]">
							<button @click="toggleDropdown" class="">
								<span v-if="isShowing">
									<svg
										width="16"
										height="16"
										viewBox="0 0 16 16"
										fill="none"
										xmlns="http://www.w3.org/2000/svg"
									>
										<path
											d="M11.9465 5.45312H7.79317H4.05317C3.41317 5.45312 3.09317 6.22646 3.5465 6.67979L6.99983 10.1331C7.55317 10.6865 8.45317 10.6865 9.0065 10.1331L10.3198 8.81979L12.4598 6.67979C12.9065 6.22646 12.5865 5.45312 11.9465 5.45312Z"
											fill="#475569"
										/>
									</svg>
								</span>

								<span v-else>
									<svg
										width="16"
										height="16"
										viewBox="0 0 16 16"
										fill="none"
										xmlns="http://www.w3.org/2000/svg"
									>
										<path
											d="M11.9465 5.45312H7.79317H4.05317C3.41317 5.45312 3.09317 6.22646 3.5465 6.67979L6.99983 10.1331C7.55317 10.6865 8.45317 10.6865 9.0065 10.1331L10.3198 8.81979L12.4598 6.67979C12.9065 6.22646 12.5865 5.45312 11.9465 5.45312Z"
											fill="#475569"
										/>
									</svg>
								</span>
							</button>
						</div>
					</div>
				</div>

				<!-- Dropdown  -->
				<div
					v-if="isShowing"
					class="w-full cursor-pointer absolute top-[100%] z-40 bg-[#FFF] max-h-[250px] overflow-y-auto mt-[8px] shadow-[0_4px_20px_rgba(101,119,149,0.2)]"
				>
					<input
						class="focus:border-transparent focus:ring-0 focus:outline-none border bg-transparent w-full text-[14px] text-[#100A37] px-[10px]"
						type="text"
						v-model="query"
						placeholder="Search"
					/>
					<!-- @click="$emit('add', column)" -->
					<ul>
						<li
							@click="addColumn(column)"
							v-for="column in filteredColumns"
							:key="column"
							class="px-[10px] py-[6px] text-[#475569] text-[13px] hover:bg-[#F5F5F5] cursor-pointer"
						>
							{{ column }}
						</li>
					</ul>
				</div>

				<!-- Commented out Column selector component  -->
				<!-- <ColumnSelector
			:columns="columns"
			:selected-columns="selectedColumns"
			@search="query = $event"
			@add="addColumn"
			@remove="removeColumn"
		/> -->
			</div>

			<button @click="toggleDropdown" class="border p-1">
				<span v-if="isShowing">Hide</span>
				<span v-else>Show</span>
			</button>

			<!-- Show Dialog button  -->
			<button
				id="show-modal"
				@click="showDialog = true"
				class="border px-[24px] py-[8px]"
			>
				Show Modal
			</button>
		</div>

		<!-- Dialog  -->
		<Dialog v-if="showDialog" @close="showDialog = false"> </Dialog>
	</div>
</template>

<script>
// import ColumnSelector from "./components/ColumnSelector.vue";
import Dialog from "./components/Dialog.vue";

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
		// ColumnSelector,
		Dialog,
	},
};
</script>

<style></style>
