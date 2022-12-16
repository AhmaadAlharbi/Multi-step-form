<template>
  <div class="flex items-baseline mt-32 mx-auto bg-white w-1/2 rounded-3xl">
    <!-- navbar col -->
    <nav
      class="
        flex flex-col
        rounded-2xl
        justify-start
        space-y-8
        text-white
        w-[274px]
        h-[568px]
      "
    >
      <!-- step one -->
      <div class="flex items-center space-x-6 mt-20">
        <div
          class="circle border rounded-full px-4 py-2 mx-3"
          :class="{ 'bg-sky-300': step == 1 }"
        >
          1
        </div>
        <div>
          <h2 class="text-gray-300 text-sm">step 1</h2>
          <h3 class="text-xl">Your info</h3>
        </div>
      </div>
      <!-- step two -->
      <div class="flex items-center space-x-6">
        <div
          class="circle border rounded-full px-4 py-2 mx-3"
          :class="{ 'bg-sky-300': step == 2 }"
        >
          2
        </div>
        <div>
          <h2 class="text-gray-300 text-sm">step 2</h2>
          <h2 class="text-xl">select plan</h2>
        </div>
      </div>
      <!-- step three -->
      <div class="flex items-center space-x-6">
        <div
          class="circle border rounded-full px-4 py-2 mx-3"
          :class="{ 'bg-sky-300': step == 3 }"
        >
          3
        </div>
        <div>
          <h2 class="text-gray-300 text-sm">step 3</h2>
          <h2 class="text-xl">add ons</h2>
        </div>
      </div>
      <!-- step foure -->
      <div class="flex items-center space-x-6">
        <div
          class="circle border rounded-full px-4 py-2 mx-3"
          :class="{ 'bg-sky-300': step == 4 }"
        >
          4
        </div>
        <div>
          <h2 class="text-gray-300 text-sm">step 4</h2>
          <h2 class="text-xl">summary</h2>
        </div>
      </div>
    </nav>
    <!-- info col -->
    <div v-if="info">
      <div class="px-20">
        <h1 class="text-4xl mb-2">Personal info</h1>
        <p class="mb-10">
          Please provide your name, email address, and phone number.
        </p>
        <form>
          <label>Name</label>
          <p
            ref="error_name"
            class="text-red-500 hidden font-bold flex-row-reverse"
          >
            This Field is required
          </p>
          <input
            type="text"
            class="block w-full border-gray-400 rounded-2xl my-2"
            ref="name"
            v-model="name"
          />

          <label>email</label>
          <p
            ref="error_email"
            class="text-red-500 hidden font-bold flex-row-reverse"
          >
            This Field is required
          </p>
          <input
            type="email"
            class="block w-full border-gray-400 rounded-2xl my-2"
            ref="email"
            v-model="email"
          />

          <label>Phone Number</label>
          <p
            ref="error_phone"
            class="text-red-500 hidden font-bold flex-row-reverse"
          >
            This Field is required
          </p>
          <input
            type="tel"
            class="block w-full border-gray-400 rounded-2xl my-2"
            v-model="phone"
            ref="phone"
          />
          <button
            @click.prevent="goToStep2"
            class="
              bg-indigo-900
              flex flex-row-reverse
              ml-auto
              text-white
              px-8
              py-2
              mt-8
            "
          >
            Next
          </button>
        </form>
      </div>
    </div>
    <!-- plan component -->
    <div v-if="plan">
      <Plan
        @goToHome="
          info = true;
          plan = false;
          step--;
        "
      />
    </div>
  </div>
</template>

<script>
import Plan from "./components/Plan.vue";
export default {
  components: { Plan },
  data() {
    return {
      info: true,
      plan: false,
      name: "",
      email: "",
      phone: "",
      step: 1,
    };
  },
  methods: {
    goToStep2() {
      // this.$refs.name.classList.remove("error");
      // this.$refs.email.classList.remove("error");
      // this.$refs.phone.classList.remove("error");
      function showRedBorder(input, errMessage) {
        input.classList.add("error");
        errMessage.classList.remove("hidden");
        errMessage.classList.add("flex");
      }
      function removeRedBorder(input, errMessage) {
        input.classList.remove("error");
        errMessage.classList.add("hidden");
        errMessage.classList.remove("flex");
      }

      if (this.name === "") {
        showRedBorder(this.$refs.name, this.$refs.error_name);
      } else if (this.email === "") {
        removeRedBorder(this.$refs.name, this.$refs.error_name);
        showRedBorder(this.$refs.email, this.$refs.error_email);
        // this.$refs.error_name.classList.add("hidden");
        // this.$refs.email.classList.add("error");
        // this.$refs.error_email.classList.remove("hidden");
        // this.$refs.error_email.classList.add("flex");
      } else {
        this.$refs.error_email.classList.add("hidden");
        this.$refs.phone.classList.add("error");
        this.$refs.error_phone.classList.remove("hidden");
        this.$refs.error_phone.classList.add("flex");
      }

      if (this.name !== "" && this.email !== "" && this.phone !== "") {
        this.step++;
        this.info = !this.info;
        this.plan = !this.plan;
      }
      // this.name === ""
      //   ? this.$refs.name.classList.add("error")
      //   : this.$refs.name.classList.remove("error");
      // this.email === ""
      //   ? this.$refs.email.classList.add("error")
      //   : this.$refs.email.classList.remove("error");
      // this.phone === ""
      //   ? this.$refs.phone.classList.add("error")
      //   : this.$refs.phone.classList.remove("error");
    },
  },
};
</script>

<style>
.error {
  border: 1px solid red;
}
</style>