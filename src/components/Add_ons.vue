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
        <p v-if="sub === 'Monthly'" class="text-gray-400">+$1/mo</p>
        <p v-else class="text-gray-400">+$10/mo</p>
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
        <p v-if="sub === 'Monthly'" class="text-gray-400">+$2/mo</p>
        <p v-else class="text-gray-400">+$20/mo</p>
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
        <p v-if="sub === 'Monthly'" class="text-gray-400">+$2/mo</p>
        <p v-else class="text-gray-400">+$20/mo</p>
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
  props: ["sub"],
  data() {
    return {
      onlineCheck: false,
      storageCheck: false,
      profileCheck: false,
      services: [],
      onlinePrice: 1,
      storagePrice: 2,
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
        if (arr.some((i) => getValue(i) === getValue(item)))
          return arr.filter((i) => getValue(i) !== getValue(item));
        else return [...arr, item];
      };

      switch (value) {
        case "online":
          this.$refs.online.classList.toggle("plan-type");
          this.onlineCheck = !this.onlineCheck;
          this.sub === "Monthly"
            ? (this.onlinePrice = 1)
            : (this.onlinePrice = 10);
          var service = {
            id: 1,
            type: "online services",
            price: this.onlinePrice,
            status: true,
          };
          this.services = toggle(this.services, service, (item) => item.id);
          // this.services.push(service);

          break;
        case "storage":
          this.$refs.storage.classList.toggle("plan-type");
          this.storageCheck = !this.storageCheck;
          // this.services = toggle(this.services, "Large Storage");
          this.sub === "Monthly"
            ? (this.storagePrice = 2)
            : (this.storagePrice = 20);
          var service = {
            id: 2,
            type: "Large Storage",
            price: this.storagePrice,
            status: true,
          };
          this.services = toggle(this.services, service, (item) => item.id);

          break;
        default:
          this.$refs.profile.classList.toggle("plan-type");

          this.profileCheck = !this.profileCheck;
          this.sub === "Monthly"
            ? (this.storagePrice = 2)
            : (this.storagePrice = 20);
          var service = {
            id: 3,
            type: "Customizable profile",
            price: this.storagePrice,
            status: true,
          };
          this.services = toggle(this.services, service, (item) => item.id);
      }
    },
    goToStep4() {
      this.$emit("step4");
      this.$emit("service-array", this.services);
    },
  },
  computed: {
    servicesTrue() {
      return this.services.filter((el) => el.status === true);
    },
  },
};
</script>

<style>
.plan-type {
  border: 1px solid rgb(0, 76, 255);
}
</style>