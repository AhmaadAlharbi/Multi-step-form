<template>
  <div class="px-20">
    <h1 class="text-4xl mb-2">Finishing up</h1>
    <p class="mb-10">Double-check everything looks OK before confirming.</p>

    <div>
      <h1 class="text-2xl capitalize">{{ typeOfPlan }} ({{ sub }})</h1>
      <div class="flex justify-between text-gray-400 mt-2 border-b pb-4">
        <h5 class="underline">Change</h5>
        <p class="text-blue-900 font-bold">${{ planPrice }}/mo</p>
      </div>
      <div v-for="service in services" :key="service">
        <div class="flex justify-between text-gray-400 mt-4">
          <h5 class="underline">{{ service.type }}</h5>
          <p class="text-blue-500 font-bold">${{ service.price }}/mo</p>
        </div>
      </div>

      <div class="flex justify-between text-gray-400 mt-8">
        <h5 class="underline">Total (Per Month)</h5>
        <p class="text-blue-900 font-bold">+${{ total }}/mo</p>
      </div>
    </div>
    <!-- buttons -->
    <div class="flex justify-between items-center mt-16">
      <button
        class="bg-transparent text-gray-400 px-8 py-2"
        @click="$emit('goToStep3')"
      >
        Go back
      </button>

      <button
        @click="$emit('step5')"
        class="bg-indigo-900 text-white px-8 py-2"
      >
        Confirm
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: ["services", "planPrice", "typeOfPlan", "sub"],
  data() {
    return {
      price: 0,
    };
  },
  computed: {
    total() {
      const result = this.services.reduce((acc, curr) => {
        acc += curr.price;
        return acc;
      }, 0);
      return result + this.planPrice;
    },
  },
};
</script>

<style>
</style>