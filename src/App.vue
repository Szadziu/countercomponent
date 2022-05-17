<template>
  <div>
    <BaseCounter
      :label="'Córki'"
      v-model.number="daughtersAmount"
      :min="1"
      :max="5"
    />
    <p>
      <BaseCounter
        :label="'Synowie'"
        v-model.number="sonsAmount"
        :min="3"
        :max="5"
      />
    </p>
  </div>
</template>

<script>
import BaseCounter from "./components/BaseCounter";

export default {
  name: "App",
  data() {
    return {
      daughtersAmount: 0,
      sonsAmount: 0
    };
  },
  components: {
    BaseCounter
  }
};
</script>
