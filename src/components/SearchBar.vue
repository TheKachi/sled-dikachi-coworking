<template>
	<div>
		<input
			class="focus:border-[#475569] focus:ring-0 focus:outline-none border bg-transparent w-full text-[14px] text-[#100A37] px-[10px]"
			type="text"
			placeholder="Search"
			:value="value"
			@input="$emit('input', $event.target.value)"
		/>
		<!-- -->
	</div>
</template>

<script>
export default {
	name: "Searchbar",
	props: ["value"],
};
</script>

<style lang="scss" scoped></style>
