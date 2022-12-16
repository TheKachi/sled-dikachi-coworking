<template>
	<div>
		<!-- Column Selector Container -->
		<div class="relative" :class="[width]">
			<!-- Label -->
			<label class="text-[#475569] text-[14px] font-bold mb-[8px]">
				{{ label }}
			</label>

			<!-- Select Dropdown -->
			<div
				:aria-label="placeholder"
				@click="toggleDropdown"
				class="text-[14px] pl-[10px] pr-[16px] py-[10px] flex items-center cursor-pointer rounded-4 z-0 bg-[#F8FAFC] focus:bg-[#F8FAFC]"
			>
				<div class="relative w-full">
					<!-- Column(s) selected  -->
					<span
						class="border p-[4px] text-xs text-[#475569] bg-[#F8FAFC] border-[#E2E8F0]"
						v-if="selected.length"
					>
						{{ selected.length }} selected
					</span>

					<!-- No column selected  -->
					<p class="text-[#475569] text-[16px]" v-else>
						{{ placeholder }}
					</p>

					<!-- Show and Hide icons  -->
					<div class="absolute -right-[12px] top-[4px]">
						<button @click="$emit('toggle')" class="">
							<div v-if="isShowing" class="rotate-180">
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
							</div>

							<div v-else>
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
							</div>
						</button>
					</div>
				</div>
			</div>

			<!-- Dropdown  -->
			<div
				v-if="isShowing"
				class="w-full cursor-pointer absolute top-[100%] z-40 bg-[#FFF] max-h-[250px] overflow-y-auto mt-[8px] shadow-[0_4px_20px_rgba(101,119,149,0.2)]"
			>
				<!-- Search  -->
				<div class="relative">
					<input
						class="focus:border-[#475569] focus:ring-0 focus:outline-none border bg-transparent w-full text-[14px] text-[#100A37] px-[10px] py-[10px]"
						type="text"
						placeholder="Search"
						:value="value"
						@input="$emit('input', $event.target.value)"
					/><button
						v-show="value !== ''"
						@click="$emit('clear-search')"
						class="absolute right-[16px] top-[12px] text-black"
					>
						<svg
							width="16"
							height="16"
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
				</div>

				<ul v-if="filtered.length > 0" class="bg-white max-h-[250px]">
					<li
						v-for="(column, i) in filtered"
						:key="i"
						@click="$emit('toggle', column)"
						class="px-[10px] py-[6px] text-[#475569] text-[13px] hover:bg-[#F5F5F5] cursor-pointer"
					>
						<span v-if="selected.includes(column)">✔️</span>
						{{ column }}
					</li>
				</ul>

				<div v-else class="h-[250px]">
					<p class="text-center mt-[80px]">No items match your search</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script>

export default {
	name: "ColumnSelector",

	props: {
		columns: {
			type: Array,
			default: () => [],
		},
		selected: {
			type: Array,
			default: () => [],
		},

		filtered: {
			type: Array,
			default: () => [],
		},
		width: {
			type: String,
			default: "w-[440px]",
		},
		placeholder: {
			type: String,
			default: "Search or select a column",
		},
		label: {
			type: String,
			default: "Multiple columns",
		},
		value: {
			type: String,
			default: "",
		},
	},
	data() {
		return {
			isShowing: false,
		};
	},
	methods: {
		toggleDropdown() {
			this.isShowing = !this.isShowing;
		},
		showDropdown() {
			this.isShowing = true;
		},

		

		close(e) {
			if (!this.$el.contains(e.target)) {
				this.isShowing = false;
			}
		},
	},
	mounted() {
		document.addEventListener("click", this.close);
	},
	beforeDestroy() {
		document.removeEventListener("click", this.close);
	},
	emits: ["toggle", "clear-search"],
};
</script>
