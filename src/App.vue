<template>
  <div id="main-app" class="container mt-4">
    <div class="justify-content-center align-items-center d-flex flex-column">
      <h4 class="title text-center text-uppercase">{{ title }}</h4>
      <AddAppointment @add="addItem" />
      <SearchAppointments
        @searchRecords="searchedAppointments"
        :myKey="filterKey"
        :myDir="filterDirection"
        @requestKey="changeKey"
        @requestDir="changeDir"
      />
      <AppointmentList
        v-bind:appointments="filteredAppointments"
        @remove="removeItem"
        @edit="editItem"
      />
    </div>
  </div>
</template>

<script>
import AppointmentList from "./components/AppointmentList.vue";
import AddAppointment from "./components/AddAppointment.vue";
import SearchAppointments from "./components/SearchAppointments.vue";

import axios from "axios";
import _ from "lodash";
export default {
  name: "MainApp",
  data() {
    return {
      title: "Appointment list",
      appointments: [],
      searchTerms: "",
      filterKey: "petName",
      filterDirection: "asc",
    };
  },
  components: { AppointmentList, AddAppointment, SearchAppointments },
  computed: {
    searchedAppointments: function () {
      return this.appointments.filter((item) => {
        return (
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.ownerName.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    },
    filteredAppointments: function () {
      return _.orderBy(
        this.searchedAppointments,
        (item) => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDirection
      );
    },
  },
  methods: {
    changeKey: function (value) {
      this.filterKey = value;
    },
    changeDir: function (value) {
      this.filterDirection = value;
    },
    searchedAppointments: function (terms) {
      this.searchTerms = terms;
    },
    removeItem: function (apt) {
      this.appointments = _.without(this.appointments, apt);
    },
    editItem: function (id, field, text) {
      const aptIndex = _.findIndex(this.appointments, { id });
      this.appointments[aptIndex][field] = text;
    },
    addItem: function (apt) {
      console.log(apt);
      apt.id = Math.floor(Math.random() * 100);
      this.appointments.push(apt);
    },
  },

  mounted() {
    (async () => {
      const response = await axios.get("/data/appointments.json");
      this.appointments = response.data;
    })();
  },
};
</script>
