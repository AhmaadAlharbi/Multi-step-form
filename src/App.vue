<template>
  <div
    class="
      flex
      items-baseline
      mt-32
      mx-auto
      bg-white
      w-1/2
      h-[600px]
      rounded-3xl
    "
  >
    <!-- navbar col -->
    <nav
      class="
        flex flex-col
        rounded-2xl
        space-y-6
        pl-6
        text-white
        w-[274px]
        h-[568px]
        mx-4
        my-3
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
        @step3="
          info = false;
          plan = false;
          addons = true;
          step++;
        "
        @plan="handlePlan"
      />
    </div>
    <!-- add-ons component -->
    <div v-if="addons">
      <Add_ons
        @goToStep2="
          step--;
          addons = false;
          plan = true;
        "
        @step4="
          addons = false;
          summary = true;
          step++;
        "
        @service-array="handleServiceArray"
        @info2="handleInfo2"
      />
    </div>
    <!-- Summary component -->
    <div v-if="summary">
      <Summary
        @goToStep3="
          addons = true;
          summary = false;
          step--;
        "
        :typeOfPlan="typeOfPlan"
        :services="services"
        :sub="sub"
        @step5="(summary = false), (thankyou = true)"
      />
    </div>
    <!-- thnakyou component -->
    <div v-if="thankyou">
      <Thankyou />
    </div>
  </div>
</template>

<script>
import Plan from "./components/Plan.vue";
import Add_ons from "./components/Add_ons.vue";
import Summary from "./components/Summary.vue";
import Thankyou from "./components/Thankyou.vue";
export default {
  components: { Plan, Add_ons, Summary, Thankyou },
  data() {
    return {
      info: true,
      plan: false,
      addons: false,
      summary: false,
      thankyou: false,
      name: "",
      email: "",
      phone: "",
      step: 1,
      typeOfPlan: "",
      sub: "",
      services: [],
    };
  },
  methods: {
    goToStep2() {
      if (this.name === "") {
        showRedBorder(this.$refs.name, this.$refs.error_name);
      } else if (this.email === "") {
        removeRedBorder(this.$refs.name, this.$refs.error_name); //to hide error message from name feild when its valid
        showRedBorder(this.$refs.email, this.$refs.error_email);
      } else {
        removeRedBorder(this.$refs.email, this.$refs.error_email); //to hide error message from email feild when its valid
        showRedBorder(this.$refs.phone, this.$refs.error_phone);
      }

      if (this.name !== "" && this.email !== "" && this.phone !== "") {
        this.step++;
        this.info = !this.info;
        this.plan = !this.plan;
      }
      //to show error message
      function showRedBorder(input, errMessage) {
        input.classList.add("error");
        errMessage.classList.remove("hidden");
        errMessage.classList.add("flex");
      }
      //to hide error message

      function removeRedBorder(input, errMessage) {
        input.classList.remove("error");
        errMessage.classList.add("hidden");
        errMessage.classList.remove("flex");
      }
    },
    handlePlan(value, value2) {
      this.typeOfPlan = value;
      this.sub = value2;
    },
    handleInfo2(value) {
      this.information = value;
    },
    handleServiceArray(value) {
      this.services = value;
    },
  },
  updated() {},
};
</script>

<style>
.error {
  border: 1px solid red;
}
</style>