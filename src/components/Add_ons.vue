<template>
  {{ information }}
  <div class="px-20">
    <h1 class="text-4xl mb-2">Pick add-ons</h1>
    <p class="mb-10">Add-ons help enhance your gaming experience.</p>
    <div class="flex flex-col justify-center items-center">
      <div
        class="
          flex
          items-center
          space-x-24
          plan-type
          rounded-3xl
          px-6
          min-w-full
          cursor-pointer
        "
        ref="online"
        @click="changeBorder('online')"
      >
        <input type="checkbox" checked v-model="onlineCheck" />
        <div class="py-3">
          <h3>Online Services</h3>
          <p>Access to multiplayer games</p>
        </div>
        <p class="text-gray-400">+$1/mo</p>
      </div>
      <div
        class="
          my-6
          min-w-full
          flex
          items-center
          space-x-24
          border
          rounded-3xl
          px-6
          cursor-pointer
        "
        ref="storage"
        @click="changeBorder('storage')"
      >
        <input type="checkbox" v-model="storageCheck" />
        <div class="py-3">
          <h3>Larger storage</h3>
          <p>Extra 1TB of cloud save</p>
        </div>
        <p class="text-gray-400">+$2/mo</p>
      </div>
      <div
        class="
          flex
          min-w-full
          items-center
          space-x-24
          border
          rounded-3xl
          px-6
          cursor-pointer
        "
        ref="profile"
        @click="changeBorder('profile')"
      >
        <input type="checkbox" v-model="profileCheck" />
        <div class="py-3">
          <h3>Customizable profile</h3>
          <p>Custom theme on your profile</p>
        </div>
        <p class="text-gray-400">+$2/mo</p>
      </div>
    </div>
    <!-- buttons -->
    <div class="flex justify-between items-center mt-8">
      <button
        class="bg-transparent text-gray-400 px-8 py-2"
        @click="$emit('goToStep2')"
      >
        Go back
      </button>

      <button @click="goToStep4" class="bg-indigo-900 text-white px-8 py-2">
        Next Step
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["information"],
  data() {
    return {
      onlineCheck: true,
      storageCheck: false,
      profileCheck: false,
      services: [],
    };
  },
  methods: {
    changeBorder(value) {
      switch (value) {
        case "online":
          this.$refs.online.classList.toggle("plan-type");

          this.onlineCheck = !this.onlineCheck;
          break;
        case "storage":
          this.$refs.storage.classList.toggle("plan-type");
          this.storageCheck = !this.storageCheck;

          break;
        default:
          this.$refs.profile.classList.toggle("plan-type");

          this.profileCheck = !this.profileCheck;
      }
    },
    goToStep4() {
      this.$emit("step4");
      let info = { type: this.selectedType, sub: this.subsicrption };
      this.plan = this.plan.push(info);
      this.$emit("info", info);
    },
  },
};
</script>

<style>
.plan-type {
  border: 1px solid rgb(0, 76, 255);
}
</style>