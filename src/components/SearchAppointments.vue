<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="input-group my-3">
      <div class="form-outline d-flex w-100 gap-3">
        <input
          type="search"
          id="searchApt"
          class="form-control"
          placeholder="Search"
          v-model="searchTerm"
        />
        <div class="input-group-append">
          <button
            type="button"
            class="btn btn-primary dropdown-toggle"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Sort By
            <span class="caret"></span>
          </button>

          <ul class="dropdown-menu dropdown-menu-right">
            <a
              @click="$emit('requestKey', 'petName')"
              class="dropdown-item d-flex justify-content-between"
              id="petName"
              href="#"
              >Pet Name<svg
                v-if="myKey === 'petName'"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                fill="currentColor"
                class="bi bi-check"
                viewBox="0 0 16 16"
              >
                <path
                  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"
                />
              </svg>
            </a>
            <a
              @click="$emit('requestKey', 'ownerName')"
              class="dropdown-item d-flex justify-content-between"
              id="ownerName"
              href="#"
              >Owner's Name<svg
                v-if="myKey === 'ownerName'"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                fill="currentColor"
                class="bi bi-check"
                viewBox="0 0 16 16"
              >
                <path
                  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"
                />
              </svg>
            </a>
            <div class="dropdown-divider"></div>
            <a
              @click="$emit('requestDir', 'asc')"
              class="dropdown-item d-flex justify-content-between"
              id="asc"
              href="#"
              >asc<svg
                v-if="myDir === 'asc'"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                fill="currentColor"
                class="bi bi-check"
                viewBox="0 0 16 16"
              >
                <path
                  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"
                />
              </svg>
            </a>
            <a
              @click="$emit('requestDir', 'desc')"
              class="dropdown-item d-flex justify-content-between"
              id="desc"
              href="#"
              >desc<svg
                v-if="myDir === 'desc'"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                fill="currentColor"
                class="bi bi-check"
                viewBox="0 0 16 16"
              >
                <path
                  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"
                />
              </svg>
            </a>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "SearchAppointments",
  data() {
    return { searchTerm: "" };
  },
  watch: {
    searchTerm: function () {
      this.$emit("searchRecords", this.searchTerm);
    },
  },
  props: ["myKey", "myDir"],
  components() {},
};
</script>
