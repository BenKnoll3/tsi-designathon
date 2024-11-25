<style></style>
<template>
  <v-app-bar :elevation="2">
    <template v-slot:prepend>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
    </template>

    <v-app-bar-title>Trans-System</v-app-bar-title>
  </v-app-bar>
  <v-card title="Employee Directory" class="w-75 mt-10 mx-auto">
    <template v-slot:text>
      <v-text-field
        v-model="search"
        label="Search by name"
        prepend-inner-icon="mdi-magnify"
        variant="outlined"
        hide-details
        single-line
      ></v-text-field>
    </template>

    <v-data-table :headers="headers" :items="payload" :search="search">
      <template v-slot:item.thumbnailURI="{ value }">
        <v-avatar size="large">
          <v-img v-bind:src="value"> </v-img>
        </v-avatar>
      </template>
    </v-data-table>
  </v-card>
</template>

<script setup lang="ts">
const payload = usePayload();
const search = ref("");

const date = useDate();

const headers = ref([
  {
    key: "thumbnailURI",
    value: (item) =>
      `${
        item.thumbnailURI
          ? item.thumbnailURI
          : "https://www.svgrepo.com/show/335455/profile-default.svg"
      }`,
  },
  {
    title: "Name",
    key: "fullName",
    value: (item) =>
      `${
        item.firstName.charAt(0).toUpperCase() +
        item.firstName.substring(1, item.firstName.length).toLowerCase()
      } ${item.lastName.toUpperCase()}`,
  },
  {
    title: "Department",
    key: "department",
    value: (item) => `${item.department ? item.department : "-"}`,
  },
  { title: "Position", key: "jobTitle" },

  {
    title: "Phone Number",
    key: "phone",
    value: (item) =>
      `${item.phone.replace(/(\d{3})(\d{3})(\d{4})/, "($1) $2-$3")}`,
  },
  { title: "Email Address", key: "email", value: "email" },
  {
    title: "Date Hired",
    key: "dateHired",
    value: (item) => `${date.format(item.dateHired, "fullDate")}`,
  },
]);
</script>
