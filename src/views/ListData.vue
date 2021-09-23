<template>
  <div class="about">
    <h1>This is a list data</h1>
    <v-app id="table">
      <v-data-table
          :headers="headers"
          :items="listItem"
          :items-per-page="5"
          class="elevator"
      >
        <!-- header-->
        <template #header.name="{header}"> {{ header.text.toUpperCase() }}</template>
        <template #header.age="{header}"> {{ header.text.toUpperCase() }}</template>
        <template #header.serial="{header}"> {{ header.text.toUpperCase() }}</template>
        <template #header.actions="{header}"> {{ header.text.toUpperCase() }}</template>
        <!--header-->

        <Icon action="abc" data="xyz"/>

      </v-data-table>
    </v-app>
  </div>
</template>

<script>
import Icon from "./Icon"
export default {
  components: {
    Icon
  },
  data: () => {
    return {
      headers: [
        {text: "name", value: 'name'},
        {text: "age", value: 'age'},
        {text: "serial", value: 'serial'},
        {text: "action", value: 'actions'}
      ],
      listItem: [
        {
          name: "ABC",
          age: 23,
          serial: "@#SSXXXXXXXXXXXX"
        },
        {
          name: "ABC",
          age: 23,
          serial: "@#SSXXXXXXXXXXXX"
        },
        {
          name: "ABC",
          age: 23,
          serial: "@#SSXXXXXXXXXXXX"
        },
      ]
    }
  }
}
</script>

<style>

</style>
