<template>
	<!-- -->
	<!-- flex flex-col h-[65vh] justify-center items-center z-50 -->
	<div
		class="fixed z-50 inset-x-0 top-[15%] overflow-y-auto"
		role="dialog"
		aria-modal="true"
	>
		<div>
			<div
				class="fixed inset-0 bg-black/60"
				aria-hidden="true"
				@click="$emit('close')"
			></div>
			<!-- <span
				class="hidden sm:inline-block sm:align-middle sm:h-screen"
				aria-hidden="true"
				>&#8203;</span
			> -->
			<div
				class="border mx-auto bg-white rounded text-left overflow-hidden shadow-[0_4px_50px_rgba(0,0,0,0.1)] transform transition-all"
				:class="[width, height]"
			>
				<div class="min-w-full min-h-full flex flex-col">
					<!-- Header  -->
					<div
						class="flex justify-between items-start bg-[#F1F5F9] px-[24px] py-[12px]"
					>
						<slot name="header"> default header </slot>
						<!-- close button  -->
						<button
							@click="$emit('close')"
							class="text-[32px] float-right"
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

					<!-- Body -->
					<div class="px-[24px] py-[12px]">
						<slot name="body"> default body </slot>
					</div>

					<!-- Footer  -->
					<div class="border mt-auto px-[24px] py-[12px]">
						<slot name="footer">
							<button
								class="modal-default-button"
								@click="$emit('close')"
							>
								OK
							</button>
						</slot>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Dialog",
	props: {
		classNames: {
			type: String,
			default: "",
		},
		width: {
			type: String,
			default: "w-screen md:w-[75%]",
		},
		height: {
			type: String,
			default: "h-screen md:h-[650px]",
		},
	},
};
</script>

<style></style>
