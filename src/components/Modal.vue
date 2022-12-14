<template>
  <div class="absolute top-0 left-0 flex justify-center items-center px-[32px] w-full h-screen bg-black/60 z-50" @click="$emit('close')">
    <div class=" bg-white rounded-sm shadow-[0_4px_50px_rgba(0,0,0,0.1)] self-center max-w-screen-md">
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
        <div class="border border-t mt-auto">
          <slot name="footer">
            <button
              class="bg-black text-white rounded"
              @click="$emit('close')"
            >
              OK
            </button>
          </slot>
        </div>
			<!-- </div> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  emits: ['close']
}
</script>

<style>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  z-index: 999;
}

.modal-content {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  padding: 20px;
}