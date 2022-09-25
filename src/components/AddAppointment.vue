<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="card text-center mt-3">
      <div
        class="card-header bg-primary text-white"
        @click="hidepanel = !hidepanel"
      >
        <span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="32"
            height="32"
            fill="currentColor"
            class="bi bi-plus"
            viewBox="0 0 16 16"
          >
            <path
              d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"
            />
          </svg>
          Add Appointment
        </span>
      </div>
    </div>

    <div class="card-body" :class="{ 'd-none': hidepanel }">
      <form id="aptForm" @submit.prevent="requestAdd">
        <div class="form-group form-row">
          <label class="col col-form-label text-md-right" for="pet-name"
            >Pet Name</label
          >
          <div class="col">
            <input
              type="text"
              class="form-control"
              name="petName"
              id="petName"
              placeholder="type pet's name..."
              v-model="formData.petName"
            />
          </div>
        </div>

        <div class="form-group form-row">
          <label class="col col-form-label text-md-right" for="owner-name"
            >Owner's Name</label
          >
          <div class="col">
            <input
              type="text"
              class="form-control"
              name="ownerName"
              id="ownerName"
              v-model="formData.ownerName"
              placeholder="type owner's name..."
            />
          </div>
        </div>
        <div class="form-group form-row">
          <label class="col col-form-label text-md-right" for="owner-name"
            >Date</label
          >
          <div class="col">
            <input
              type="date"
              class="form-control"
              name="date"
              id="date"
              v-model="formData.date"
              placeholder="type appointment date..."
            />
          </div>
        </div>
        <div class="form-group form-row">
          <label class="col col-form-label text-md-right" for="owner-name"
            >Time</label
          >
          <div class="col">
            <input
              type="time"
              class="form-control"
              name="time"
              id="time"
              v-model="formData.time"
              placeholder="type appointment time..."
            />
          </div>
        </div>
        <div class="d-flex justify-content-end">
          <button type="submit" class="btn btn-primary p-2 m-2">
            Add Appointment
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddAppointment",
  methods: {
    requestAdd: function () {
      this.formData = {
        petName: this.formData.petName,
        ownerName: this.formData.ownerName,
        date: Date.parse(this.formData.date + " " + this.formData.time),
      };
      this.$emit("add", this.formData);
      this.formData = [];
      this.hidepanel = true;
    },
  },

  data() {
    return {
      hidepanel: true,
      formData: [],
    };
  },
};
</script>

<style>
.card-header {
  cursor: pointer;
}
</style>
