<template>
  <div>
    <label :for="label">{{ label }}</label>
    <div class="counter" :class="{ focused: isInputFocused }">
      <button @click="counterChange(value - 1)">-</button>
      <input
        :id="label"
        :name="label"
        type="number"
        :value="value"
        :min="min"
        :max="max"
        @input="
          ev => {
            counterChange(ev.target.value);
          }
        "
        @focus="toggleFocus"
        @blur="toggleFocus"
      />
      <button @click="counterChange(value + 1)">+</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String
    },
    value: {
      type: Number
    },
    min: {
      type: Number
    },
    max: {
      type: Number
    }
  },

  data() {
    return {
      isInputFocused: false
    };
  },

  methods: {
    toggleFocus({ target }) {
      if (target.value <= this.max && target.value >= this.min) {
        this.$emit("input", target.value);
      }
      this.isInputFocused = !this.isInputFocused;
      return;
    },

    counterChange(val) {
      console.log(val);

      if (val === "") {
        console.log("change");
        this.$emit("input", "0");
        return;
      }

      let checkedValue = val;
      if (checkedValue <= this.max && checkedValue >= this.min) {
        this.$emit("input", checkedValue);
      }
      return;
    }
  },

  mounted() {
    this.$emit("input", this.min);
  }
};
</script>

<style>
.counter {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: "Domine", serif;
  width: 311px;
  height: 64px;
  border: 1px rgba(29, 45, 74, 0.2) solid;
}

.focused {
  background-color: rgb(224, 185, 125, 0.15);

  border-color: #bf934f;
}

label {
  font-family: "Domine", serif;
}

input {
  font-size: 13px;
  line-height: 19.5px;
  font-weight: 400;
  text-align: center;
  color: #1d2d4a;
  border: none;
  outline: none;
  width: 22px;
  height: 20px;
  background-color: transparent;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

button {
  padding: 0;
  width: 40px;
  height: 40px;
  background-color: rgba(29, 45, 74, 0.1);
  border: none;
  font-size: 25px;
  color: #1d2d4a;
  margin: 12px;
  cursor: pointer;
}
</style>
