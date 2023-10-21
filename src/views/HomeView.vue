<script setup>
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
  ]

  const getImageUrl = (name) => {
        return (`/images/${name}.png`)
    }
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
      <div class="row w-100 my-5">
        <div class="col-12 col-md-6 rounded-4 bg-danger p-5 text-white text-start d-flex align-items-center">
          <div>
            <p class="big-text">
              READY TO START YOUR DAY?
            </p>
            <p class="semi-big-text">  
              WHAT DO YOU WANT TO DO TODAY?
            </p>
          </div>
        </div>
        <div class="col-12 col-md-6 p-1 p-md-0 px-md-5 mt-4 mt-md-0">
          <form>
            <div class="mb-3">
              <label for="activity-title" class="form-label">Title</label>
              <input type="text" class="form-control" id="activity-title" aria-describedby="activityHelp">
              <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <div class="mb-3">
              <label for="exampleInputPassword1" class="form-label">Password</label>
              <input type="password" class="form-control" id="exampleInputPassword1">
            </div>
            <div class="mb-3 form-check">
              <input type="checkbox" class="form-check-input" id="exampleCheck1">
              <label class="form-check-label" for="exampleCheck1">Check me out</label>
            </div>
            <button type="submit" class="btn btn-primary float-end">Submit</button>
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
