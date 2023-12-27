<template>
  <CComponent>
    <template v-slot:default="slotProps">
      <slot v-bind="slotProps"/>
    </template>
  </CComponent>
</template>

<script>
import CComponent from "@/components/C";

export default {
  name: 'B-component',
  components: {
    CComponent,
  },
  data() {
    return {
      msg: 'test'
    };
  }
};
</script>

<style scoped>

</style>
