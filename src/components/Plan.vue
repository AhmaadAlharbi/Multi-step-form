<template>
  <div class="px-20">
    <h1 class="text-4xl mb-2">Select your plan</h1>
    <p class="mb-10">You have the option of monthly or yearly billing.</p>
    <div class="grid grid-cols-3 gap-16">
      <!-- arcade col -->
      <div class="px-10 py-5 border rounded-3xl space-y-5">
        <img src="../assets/images/icon-arcade.svg" alt="" />
        <div>
          <h1>Arcade</h1>
          <p>$9/Mo</p>
        </div>
      </div>
      <!-- Advanced col -->
      <div class="px-10 py-5 border rounded-3xl space-y-5">
        <img src="../assets/images/icon-advanced.svg" alt="" />
        <div>
          <h1>Advanced</h1>
          <p>$12/Mo</p>
        </div>
      </div>
      <!-- Pro col -->
      <div class="px-10 py-5 border rounded-3xl space-y-5">
        <img src="../assets/images/icon-pro.svg" alt="" />
        <div>
          <h1>Pro</h1>
          <p>$15/Mo</p>
        </div>
      </div>
    </div>
    <!-- switch -->
    <div class="mt-10 flex justify-center items-center space-x-10">
      <p>Monthly</p>
      <label class="switch">
        <input type="checkbox" />
        <span class="slider round"></span>
      </label>
      <p>Yearly</p>
    </div>
    <!-- buttons -->
    <div class="flex justify-between items-center mt-20">
      <button
        class="bg-transparent text-gray-400 px-8 py-2"
        @click="$emit('goToHome')"
      >
        Go back
      </button>

      <button type="submit" class="bg-indigo-900 text-white px-8 py-2">
        Next Step
      </button>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}
.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #2196f3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196f3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>