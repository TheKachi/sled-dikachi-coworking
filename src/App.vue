<template>
	<div id="app" class="w-screen h-screen overflow-hidden">
		<!-- Column Selector Container -->
		<div
			class="md:mx-auto mt-[100px] px-[24px] md:px-[200px] flex flex-col md:flex-row gap-[40px] md:gap-[60px] items-start"
		>
			<div class="flex flex-col gap-[24px]">
				<ColumnSelector
					:columns="unselectedOrders"
					:selected="selectedOrders"
					:filtered="filteredOrders"
					@toggle="toggleColumn"
					@clear-search="clearColumnSearch"
					v-model="orderQuery"
					width="w-[300px]"
					placeholder="Search or select Order checks"
				/>

				<ColumnSelector
					:columns="unselectedCoupons"
					:selected="selectedCoupons"
					:filtered="filteredCoupons"
					@toggle="
						() => toggle(column, selectedCoupons, unselectedCoupons)
					"
					@clear-search="couponQuery = ''"
					v-model="couponQuery"
					width="w-[300px]"
					placeholder="Search or select Coupon checks"
					label="Another multiple column"
				/>
			</div>

			<!-- Modal buttons  -->
			<div class="flex flex-col gap-[24px]">
				<button
					@click="showModalWithFooter = true"
					class="border px-[24px] py-[4px]"
				>
					Show Modal With footer
				</button>
				<button
					@click="showModalNoFooter = true"
					class="border px-[24px] py-[4px]"
				>
					Show Modal without footer
				</button>
				<button
					@click="showModalLgContent = true"
					class="border px-[24px] py-[4px]"
				>
					Show Modal with a lot of content
				</button>
			</div>
		</div>

		<!-- Modal with footer -->
		<Modal
			:isActive="showModalWithFooter"
			@close="showModalWithFooter = false"
		>
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
					<ColumnSelector
						:columns="unselectedOrders"
						:selected="selectedOrders"
						:filtered="filteredOrders"
						@toggle="toggleColumn"
						@clear-search="clearColumnSearch"
						v-model="orderQuery"
					/>
				</div>
			</div>

			<div slot="footer">
				<div class="flex justify-end gap-[8px] p-[24px]">
					<button
						class="border px-[24px] py-[4px]"
						@click="showModalWithFooter = false"
					>
						Cancel
					</button>

					<button
						class="bg-black text-white px-[24px] py-[4px]"
						@click="showModalWithFooter = false"
					>
						Save
					</button>
				</div>
			</div>
		</Modal>

		<!-- Modal with no footer -->
		<Modal :isActive="showModalNoFooter" @close="showModalNoFooter = false">
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
					<ColumnSelector
						:columns="unselectedOrders"
						:selected="selectedOrders"
						:filtered="filteredOrders"
						@toggle="toggleColumn"
						@clear-search="clearColumnSearch"
						v-model="orderQuery"
					/>
				</div>
			</div>
		</Modal>

		<!-- Modal with a lot of content  -->
		<Modal :isActive="showModalLgContent" @close="showModalLgContent = false">
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
					<ul v-if="filteredOrders.length > 0" class="bg-white h-full">
						<li
							v-for="column in filteredOrders"
							:key="column"
							class="px-[10px] py-[6px] text-[#475569] text-[13px] hover:bg-[#F5F5F5] cursor-pointer"
						>
							{{ column }}
						</li>
						<li
							v-for="column in filteredOrders"
							:key="column"
							class="px-[10px] py-[6px] text-[#475569] text-[13px] hover:bg-[#F5F5F5] cursor-pointer"
						>
							{{ column }}
						</li>
					</ul>
				</div>
			</div>

			<div slot="footer">
				<div class="flex justify-end gap-[8px] p-[24px]">
					<button
						class="border px-[24px] py-[4px]"
						@click="showModalLgContent = false"
					>
						Cancel
					</button>

					<button
						class="bg-black text-white px-[24px] py-[4px]"
						@click="showModalLgContent = false"
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
			coupons: ["ID", "Total", "Links", "Number"],
			selectedOrders: [],
			selectedCoupons: [],
			unselectedOrders: [],
			unselectedCoupons: [],
			orderQuery: "",
			couponQuery: "",
			isShowing: false,
			showModalWithFooter: false,
			showModalNoFooter: false,
			showModalLgContent: false,
		};
	},

	methods: {
		// add column to selectedOrders array
		toggleColumn(column) {
			// remove from selected array
			if (this.selectedOrders.includes(column)) {
				this.removeColumn(column);
			} else {
				this.addColumn(column);
			}
		},

		toggle(col, selectedArray, unselectedArray) {
			if (selectedArray.includes(col)) {
				// this.remove(col, selectedArray, unselectedArray);
				selectedArray = selectedArray.filter((c) => c !== column);

				// push to unselected array
				unselectedArray.unshift(column);
			} else {
				// this.add(col, selectedArray, unselectedArray);
				selectedArray.push(col);
				unselectedArray = unselectedArray.filter((c) => c !== column);
			}
			this.clearSearch();
		},

		add(col, selectedArray, unselectedArray) {
			selectedArray.push(col);
			unselectedArray = unselectedArray.filter((c) => c !== column);

			this.clearSearch();
		},

		remove(col, selectedArray, unselectedArray) {
			selectedArray = selectedArray.filter((c) => c !== col);

			// push to unselected array
			unselectedArray.unshift(col);

			this.clearSearch();
		},

		// add column to selectedOrders array and move to the top
		addColumn(column) {
			this.selectedOrders.push(column);
			this.unselectedOrders = this.unselectedOrders.filter(
				(c) => c !== column
			);

			this.clearSearch();
		},

		// remove column from selectedOrders array and move to the bottom
		removeColumn(column) {
			this.selectedOrders = this.selectedOrders.filter((c) => c !== column);

			// push to unselected array
			this.unselectedOrders.unshift(column);

			this.clearSearch();
		},

		clearColumnSearch() {
			this.orderQuery = "";
		},
	},

	computed: {
		// return the column that matches the search orderQuery
		filteredOrders() {
			let columns = this.selectedOrders.concat(this.unselectedOrders);
			if (this.orderQuery !== "") {
				return columns.filter((column) =>
					column.toLowerCase().includes(this.orderQuery.toLowerCase())
				);
			} else return columns;
		},

		filteredCoupons() {
			let columns = this.selectedCoupons.concat(this.unselectedCoupons);
			if (this.couponQuery !== "") {
				return columns.filter((column) =>
					column.toLowerCase().includes(this.couponQuery.toLowerCase())
				);
			} else return columns;
		},
	},

	components: {
		Modal,
		ColumnSelector,
	},

	mounted() {
		this.unselectedOrders = this.columns;
		this.unselectedCoupons = this.coupons;
	},
};
</script>

<style></style>
