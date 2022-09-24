<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <h4 class="title text-center text-uppercase">{{ title }}</h4>
      <AddAppointment />
      <AppointmentList
        v-bind:appointments="appointments"
        @remove="removeItem"
        @edit="editItem"
      />
    </div>
  </div>
</template>

<script>
import AppointmentList from "./components/AppointmentList.vue";
import AddAppointment from "./components/AddAppointment.vue";
import axios from "axios";
import _ from "lodash";
export default {
  name: "MainApp",
  components: { AppointmentList, AddAppointment },
  methods: {
    removeItem: function (apt) {
      this.appointments = _.without(this.appointments, apt);
    },
    editItem: function (id, field, text) {
      const aptIndex = _.findIndex(this.appointments, { id });
      this.appointments[aptIndex][field] = text;
    },
  },
  data() {
    return {
      title: "Appointment list",
      appointments: [],
    };
  },
  mounted() {
    (async () => {
      const response = await axios.get("/data/appointments.json");
      this.appointments = response.data;
    })();
  },
};
</script>
