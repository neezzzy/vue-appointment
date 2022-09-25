<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div
        class="list-group-item d-flex align-items-start"
        v-for="item in appointments"
        v-bind:key="item.id"
      >
        <button
          @click="$emit('remove', item)"
          class="btn btn-sm m-2 p-2 btn-danger"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="16"
            height="16"
            fill="currentColor"
            class="bi bi-trash-fill"
            viewBox="0 0 16 16"
          >
            <path
              d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"
            />
          </svg>
        </button>
        <div class="w-100">
          <div class="d-flex justify-content-between">
            <span
              contenteditable="true"
              @blur="$emit('edit', item.id, 'petName', $event.target.innerText)"
              class="h4 text-primary"
              >{{ item.petName }}</span
            >
            <span class="mr-auto">{{ formatDate(item.date) }}</span>
          </div>
          <div class="owner-name">
            <span class="font-weight-bold text-primary mr-1">Owner:</span>
            <span
              contenteditable="true"
              @blur="
                $emit('edit', item.id, 'ownerName', $event.target.innerText)
              "
              class="m-1"
              >{{ item.ownerName }}</span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "AppointmentList",
  props: ["appointments"],
  methods: {
    formatDate: function (date) {
      return moment.unix(date).format("DD/MM ddd hh:mm A");
    },
  },
};
</script>
