<template>
	<div
		class="fixed top-60 z-[100] inset-0 overflow-y-auto"
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
				class="mx-auto bg-white text-left rounded-lg overflow-hidden shadow-[0_4px_50px_rgba(0,0,0,0.1)] transform transition-all"
				:class="[width, height]"
			>
				<div
					class="px-[24px] py-[12px] min-w-full min-h-full flex flex-col"
					:class="[width, height]"
				>
					<!-- Header  -->
					<div class="flex justify-between items-center">
						<slot name="header"> default header </slot>
						<button
							@click="$emit('close')"
							class="text-[32px] float-right"
						>
							x
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
			default: "w-[500px]",
		},
		height: {
			type: String,
			default: "h-[500px]",
		},
	},
};
</script>

<style></style>
