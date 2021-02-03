<template>
  <div class="mb-3">
    <label :for="lowerName" class="form-label">{{ name }}</label>
    <div class="input-group">
      <input
        v-bind="$attrs"
        :class="value.length <= 0 ? 'empty' : null"
        class="form-control"
        v-model="value"
        :id="lowerName"
        @change="$emit('change', value)"
        @blur="recheck"
      />
    </div>
    <p v-if="error" class="text-danger fs-6 ps-2">{{ error }}</p>
  </div>
</template>

<script>
export default {
  name: "InputGroup",
  inheritAttrs: false,
  props: {
    name: {
      type: String,
      default: "Input",
    },
  },
  data() {
    return {
      lowerName: null,
      value: "",
      error: null,
    };
  },
  mounted() {
    this.lowerName = this.name.toLowerCase();
  },
  methods: {
    handleInvalid(event) {
      event.target.checkValidity();
      console.log(event.target.checkValidity());
      this.setValidationMsg(event.target);
      this.error = event.target.validationMessage;
    },
    recheck(event) {
      if (event.target.checkValidity()) {
        this.error = null;
      } else {
        this.handleInvalid(event);
      }
    },
    setValidationMsg(input) {
      if (input.validity.typeMismatch) {
        input.setCustomValidity("El valor no es del tipo indicado");
      }
      if (input.validity.patternMismatch) {
        input.setCustomValidity("El valor no cumple con las necesidades");
      }
      if (input.validity.tooLong) {
        input.setCustomValidity("El contenido es muy largo");
      }
      if (input.validity.tooShort) {
        input.setCustomValidity("El contenido es muy corto");
      }
      if (input.validity.rangeUnderflow) {
        input.setCustomValidity("El valor es menor al minimo");
      }
      if (input.validity.rangeOverflow) {
        input.setCustomValidity("El valor es mayor al maximo");
      }
      if (input.validity.stepMismatch) {
        input.setCustomValidity("Step");
      }
    },
  },
};
</script>

<style scoped>
input:not(.empty):valid {
  border-color: greenyellow;
  color: greenyellow;
}
input:not(.empty):invalid {
  border-color: red;
  color: red;
}
input:not(.empty)[invalid] {
  border-color: red;
  color: red;
}
</style>
