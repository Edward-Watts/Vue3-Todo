<script setup>
import { ref } from 'vue';

const date = ref();

const time = ref({
  hours: new Date().getHours(),
  minutes: new Date().getMinutes()
});

  const info = [
    {
      img: "list-icon",
      title: "Create Activities",
      subtitle:"Create a list of activities for Easy Tracking"
    },
    {
      img: "calendar",
      title: "Set Date",
      subtitle:"Add date and time for prompt action"
    },
    {
      img: "check-mark",
      title: "Easy to use",
      subtitle:"Friendly and functional user interface"
    }
  ];

  const getImageUrl = (name) => {
        return (`/images/${name}.png`)
    };
  
  
</script>

<template>
  <main>
    <div class="container d-grid mt-3 mt-md-5" style="justify-items: center;">
      <div class="row d-flex justify-content-between w-100">
        <div class="card d-flex justify-content-center align-items- rounded-4 primary p-3 mt-3 mt-md-0" style="height: 7rem; width: 24rem;" v-for="(item, i) in info" :key="i">
          <div class="col d-flex align-items-center">
            <div class="me-4">
              <img :src="getImageUrl(item.img)" height="60" width="60" />
            </div>
            <div>
              <p class="title">{{ item.title }}</p>
              <p class="subtitle">
                {{ item.subtitle }}
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="row w-100 d-block d-md-flex justify-content-between my-5">
        <div class="col-12 col-md-4 rounded-4 bg-danger p-5 text-white text-start d-flex align-items-center">
          <div>
            <p class="big-text">
              READY TO START YOUR DAY?
            </p>
            <p class="semi-big-text">  
              WHAT DO YOU WANT TO DO TODAY?
            </p>
          </div>
        </div>
        <div class="col-12 col-md-7 p-1 border rounded-4 mt-4 mt-md-0">
          <form class="d-block d-md-flex p-3">
            <div class="col-12 col-md-8 ps-0 ps-md-0">
              <div class="mb-3">
                <label for="activity-title" class="form-label">Title</label>
                <input type="text" class="form-control" id="activity-title" aria-describedby="activityHelp">
                <div id="activityHelp" class="form-text">Example: Go to Walmart.</div>
              </div>
              <div class="mb-3">
                <label for="activity-details" class="form-label">Details</label>
                <textarea class="form-control" id="activity-details"></textarea>
              </div>
            </div>
            
            <div class="col-12 col-md-4 ps-md-4">      
              <div class="mb-3">
                <label for="activity-date" class="form-label">Date</label>
                <VueDatePicker v-model="date"></VueDatePicker>
              </div>
              <div class="mb-3">
                <label for="activity-timie" class="form-label">Time</label>
                <VueDatePicker v-model="time" time-picker/>
              </div>
              <div> 
                <button type="submit" class="btn btn-dark px-5 py-2 w-100">Save Activity</button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.title {
  font-size: large;
  font-weight: 700;
}
.subtitle {
  margin-top: -12px;
  font-size: smaller;
  font-weight: 300;
}

.big-text {
  font-size: 38px;
  font-weight: 800;
}

.semi-big-text {
  margin-top: -12px;
  font-size: larger;
}
</style>
