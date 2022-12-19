<template>
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
  data() {
    return {
      onlineCheck: true,
      storageCheck: false,
      profileCheck: false,
      services: ["Online Services"],
    };
  },
  methods: {
    changeBorder(value) {
      // to check if value in array , if yes delete the value , if not add the value
      //source from https://dev.to/reobin/how-to-toggle-an-item-in-a-javascript-array-5dl5
      const removeAtIndex = (arr, index) => {
        const copy = [...arr];
        copy.splice(index, 1);
        return copy;
      };

      const toggle = (arr, item, getValue = (item) => item) => {
        const index = arr.findIndex((i) => getValue(i) === getValue(item));
        if (index === -1) return [...arr, item];
        return removeAtIndex(arr, index);
      };

      switch (value) {
        case "online":
          this.$refs.online.classList.toggle("plan-type");
          this.onlineCheck = !this.onlineCheck;
          this.services = toggle(this.services, "Online Services");

          break;
        case "storage":
          this.$refs.storage.classList.toggle("plan-type");
          this.storageCheck = !this.storageCheck;
          this.services = toggle(this.services, "Large Storage");

          break;
        default:
          this.$refs.profile.classList.toggle("plan-type");

          this.profileCheck = !this.profileCheck;
          this.services = toggle(this.services, "Customizable profile");
      }
    },
    goToStep4() {
      this.$emit("step4");
      this.$emit("service-array", this.services);
    },
  },
};
</script>

<style>
.plan-type {
  border: 1px solid rgb(0, 76, 255);
}
</style>