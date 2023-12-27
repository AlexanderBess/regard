<template>
  <div>
    <BComponent>
      <template v-slot:default="slotProps">
        <p> {{ slotProps.msg }} </p>
      </template>
    </BComponent>
  </div>
</template>

<script>
import BComponent from "@/components/B";

export default {
  name: 'A-component',
  components: {
    BComponent
  }
};
</script>

<style scoped>

</style>
