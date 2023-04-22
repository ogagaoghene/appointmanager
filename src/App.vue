<template>
  <div id="main-app" class="container-fluid p-4">
    <div class="row justify-content-center">
      <appointment-list :appointments="appointments" @remove="removeItem"/>
    </div>
  </div>
</template>

<script>
import  AppointmentList  from "./components/AppointmentList"
import axios from 'axios';
import _ from "lodash";

export default {
  name: 'App',
  data() {
    return {
      appointments: [],
      appointmentIndex: 0
    }
  },
  components: {
    AppointmentList
  },
  mounted() {
    axios.get("./data/appointments.json")
          .then(response => (this.appointments = response.data.map(item => {
            item.appointmentId = this.appointmentIndex;
            this.appointmentIndex++;
            return item;
          })))
  },
  methods: {
    removeItem: function(appointment) {
      this.appointments = _.without(this.appointments, appointment)
    }
  }
}
</script>
