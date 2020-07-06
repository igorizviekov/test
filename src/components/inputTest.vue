<template>
  <div class="input">
    <label :for="fieldProp">{{ labelProp }}:</label>

    <input
      v-if="fieldProp !== 'gender'"
      :name="fieldProp"
      :type="typeProp"
      :value="valueProp"
      @input="handleInput($event, fieldProp)"
    />

    <select v-else :name="fieldProp" @input="handleInput($event, fieldProp)">
      <option
        v-for="(option, index) in optionsProp"
        :key="index"
        :value="option.value"
      >{{ option.label }}</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    typeProp: {
      type: String,
      default: "text"
    },
    valueProp: {
      type: String,
      default: ""
    },
    fieldProp: {
      type: String,
      default: ""
    },
    labelProp: {
      type: String,
      default: ""
    },
    optionsProp: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    handleInput($event, input) {
      if (input === "name") {
        const payload = {
          type: input,
          val: $event.target.value
        };
        this.$emit("inputUpdate", payload);
      }
      if (input === "gender") {
        const payload = {
          type: input,
          val: $event.target.value
        };
        this.$emit("inputUpdate", payload);
      }
      if (input === "sub") {
        const payload = {
          type: input,
          val: $event.target.value
        };
        this.$emit("inputUpdate", payload);
      }
    }
  }
};
</script>
<style scoped>
.input {
  margin: 10px;
  display: flex;
  justify-content: start;
}
label {
  margin-right: 5px;
}
</style>
