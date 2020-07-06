<template>
  <div class="testfForm">
    <h1>Form</h1>
    <h4 v-if="error">{{ errors }}</h4>
    <h3 v-if="success">User successfully updated!</h3>
    <div class="inputContainer">
      <test-input
        :type-prop="userFields[0].type"
        :field-prop="userFields[0].field"
        :label-prop="userFields[0].label"
        :value-prop="userData.name"
        @inputUpdate="updateUser"
      />
      <test-input
        :type-prop="userFields[1].type"
        :field-prop="userFields[1].field"
        :label-prop="userFields[1].label"
        :options-prop="userFields[1].meta.values"
        :value-prop="userData.gender"
        @inputUpdate="updateUser"
      />
      <test-input
        :type-prop="userFields[2].type"
        :field-prop="userFields[2].field"
        :label-prop="userFields[2].label"
        :value-prop="userData.sub"
        @inputUpdate="updateUser"
      />
    </div>
    <button :disabled="error" @click="update">UPDATE</button>
  </div>
</template>

<script>
import testInput from "../components/inputTest";
export default {
  name: "form",
  components: { testInput },
  data() {
    return {
      error: false,
      errors: null,
      success: false,
      userFields: [
        {
          label: "Name",
          field: "name",
          type: "string",
          validator: "nameValidator"
        },
        {
          label: "Gender",
          field: "gender",
          type: "select",
          validator: "genderValidator",
          meta: {
            values: [
              {
                label: "Male",
                value: "male"
              },
              {
                label: "Female",
                value: "female"
              },
              {
                label: "Alien",
                value: "alien"
              }
            ]
          }
        },
        {
          label: "Subscription",
          field: "sub",
          type: "date",
          validator: "dateValidator"
        }
      ],
      userData: {
        name: "User Name",
        gender: "male",
        sub: "2020-03-04"
      }
    };
  },
  methods: {
    updateUser({ type, val }) {
      this.success = false;
      if (type === "name") {
        this.error = false;
        this.userData.name = val;
      }
      if (type === "gender") {
        this.error = false;
        this.userData.gender = val;
      }
      if (type === "sub") {
        this.error = false;
        this.userData.sub = val;
      }
    },
    update() {
      this.validate();
      if (!this.error) {
        console.log(this.userData);
        this.success = true;
      }
    },
    validate() {
      //validate name
      if (this.userData.name.length < 2) {
        this.errors = "Name required.";
        return (this.error = true);
      }
      //validate gender
      if (this.userData.gender === "alien") {
        this.errors = "Only humans accepted.";
        return (this.error = true);
      }
      //validate date
      if (this.userData.sub) {
        const parts = this.userData.sub.split("-");
        const year = parseInt(parts[0]);
        const month = parseInt(parts[1]);
        if (year < 2020 || year > 2030 || month === 0 || month > 12) {
          this.errors = "Date is not valid.";
          return (this.error = true);
        }
      }
    }
  }
};
</script>
<style scoped>
.inputContainer {
  width: 20%;
  margin: auto;
}
button {
  cursor: pointer;
}
h4 {
  color: red;
}
h3 {
  color: green;
}
</style>
