<template>
	<div
		class="fixed top-60 z-50 inset-0 overflow-y-auto"
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
				class="mx-auto bg-white text-left overflow-hidden shadow-[0_4px_50px_rgba(0,0,0,0.1)] transform transition-all"
				:class="[width, height]"
			>
				<div
					class="px-[24px] py-[12px] min-w-full min-h-full flex flex-col"
				>
					<!-- Header  -->
					<div class="flex justify-between items-center">
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
					<div class="">
						<slot name="body"> default body </slot>
					</div>

					<!-- Footer  -->
					<div class="modal-footer border mt-auto">
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
			default: "w-screen md:w-1/2",
		},
		height: {
			type: String,
			default: "h-screen md:h-[500px]",
		},
	},
};
</script>

<style></style>
