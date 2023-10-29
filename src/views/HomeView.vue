<script>
import { defineComponent, reactive, onMounted } from 'vue';
import { Icon } from '@iconify/vue';
import TableLite from "vue3-table-lite";
import moment from "moment";

// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAnalytics } from "firebase/analytics";
import { getDatabase, ref, set, push } from "firebase/database";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyBrQRhU7eF5kLtRNDFaQVJn2QqZF55OxDo",
  authDomain: "todo-1a3cf.firebaseapp.com",
  projectId: "todo-1a3cf",
  storageBucket: "todo-1a3cf.appspot.com",
  messagingSenderId: "219498716511",
  appId: "1:219498716511:web:3e6265966b1fb0a64ceaea",
  measurementId: "G-H3MKX6DTHL"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const analytics = getAnalytics(app); 

export default defineComponent({
  name: "HomeView",
  components: { TableLite },
  setup() {
    const infoState = reactive({
      info: [
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
        ]
    });

    const activitState = reactive({
      activity: [
      {
        num: 1,
        title: 'Go to Gym',
        description: 'Complete 30 biceps reps',
        date: '20-10-23',
        time: {
          hours: 9,
          minutes: 30
        }
      },
      {
        num: 2,
        title: 'Grab groceries at Walmart',
        description: 'Complete 30 biceps reps',
        date: '20-10-23',
        time: {
          hours: 9,
          minutes: 30
        }
      }
      ]
    })
    
    // Table config
    const table = reactive({
      isLoading: false,
      columns: [
        {
          
          label: "No.",
          field: "num",
          width: "3%",
          isKey: true,
        },
        {
          label: "Title",
          field: "title",
          width: "10%",
        },
        {
          label: "Description",
          field: "description",
          width: "15%",
        },
        {
          label: "Date",
          field: "date",
          width: "15%",
        },
        {
          label: "Time",
          field: "time",
          width: "15%",
        }
      ],
      rows: [],
      totalRecordCount: 0,
    });

    const getImageUrl = (name) => {
        return (`/images/${name}.png`)
    };
    /**
     * Loading Activities
     */
      const getActivities = () => {
      table.isLoading = true;
      setTimeout(() => {
        if (activitState.activity) {
          table.rows = activityData();
        }
        table.totalRecordCount = activitState.activity.length;
      }, 600);
    };

    const eventState = reactive({
      event: {
        num: 0,
        title: '',
        description: '',
        date: '',
        time: ''
      },
    })

    const activityData = () => {
      let data = activitState.activity
      return data;
    };

    const saveActivity = (el) => {
      if (!el.title || !el.description || !el.date || !el.time) {
        alert("Please complete all fields")
        return
      }
      
      const db = getDatabase();
      const activityRef = ref(db, 'activities/ ' + el.title)
      const newActivity = push(activityRef)
      set(newActivity, {
        title: el.title,
        description: el.description,
        date: moment(el.date).format("L"),
        time: el.time
      })
      eventState.event.title = ""
      eventState.event.description = ""
      eventState.event.date = ""
      eventState.event.time = ""
    }
    // First get data
    getActivities();

    return {
      table,
      infoState,
      activitState,
      eventState,
      getActivities,
      getImageUrl,
      saveActivity
    };
  }
})

/*-----------------------------------------------------------------------------------------------*/
</script>

<template>
  <main>
    <div class="container d-grid mt-3 mt-md-5" style="justify-items: center;">
      <div class="row d-flex justify-content-between w-100">
        <div class="card d-flex justify-content-center align-items- rounded-4 primary p-3 mt-3 mt-md-0" style="height: 7rem; width: 24rem;" v-for="(item, i) in infoState.info" :key="i">
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
        <div class="col-12 col-md-7 p-1 border rounded-4 mt-4 mt-md-0" v-for="(event , i) in eventState" :key="i">
          <div class="d-block d-md-flex p-3">
            <div class="col-12 col-md-8 ps-0 ps-md-0">
              <div class="mb-3">
                <label for="activity-title" class="form-label">Title</label>
                <input type="text" class="form-control" id="activity-title" v-model="event.title" aria-describedby="activityHelp">
                <div id="activityHelp" class="form-text">Example: Go to Walmart.</div>
              </div>
              <div class="mb-3">
                <label for="activity-details" class="form-label">Details</label>
                <textarea class="form-control" id="activity-details" v-model="event.description"></textarea>
              </div>
            </div>
            
            <div class="col-12 col-md-4 ps-md-4">      
              <div class="mb-3">
                <label for="activity-date" class="form-label">Date</label>
                <VueDatePicker v-model="event.date" :enable-time-picker="false"></VueDatePicker>
              </div>
              <div class="mb-3">
                <label for="activity-timie" class="form-label">Time</label>
                <VueDatePicker v-model="event.time" time-picker/>
              </div>
              <div> 
                <button class="btn btn-dark px-5 py-2 w-100" @click="saveActivity(event)">Save Activity</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="row w-100 my-4"> 
        <div class="col-12 d-flex align-items-center justify-content-start">
          <h4 class="text-start">
            Activities
          </h4>
        </div>
        <div class="col-12">
          <table-lite
            :is-slot-mode="true"
            :is-fixed-first-column="true"
            :max-height="300"
            :is-loading="table.isLoading"
            :columns="table.columns"
            :rows="table.rows"
            :total="table.totalRecordCount"
            :sortable="table.sortable"
            :messages="table.messages"
            @is-finished="table.isLoading = false"
          >
          <template v-slot:time="data">
            {{ data.value.time.hours }}:{{ data.value.time.minutes }}
          </template>
        </table-lite>
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
