<template #item.actions="{}">
  <div>
    <v-icon
        small
        class="mr-2"
    >
      mdi-pencil
    </v-icon>
    <v-icon
        small
        class="mr-2"
    >
      mdi-delete
    </v-icon>
    <span>{{ action }}</span>
  </div>
</template>
<script>
  export default {
    name: "Icon",
    props: {
      action: String,
      data: String
    }
  }
</script>

<style>

</style>
