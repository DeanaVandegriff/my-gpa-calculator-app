<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newCoursesParams: {},
      errors: [],
    };
  },
  methods: {
    createCourse: function () {
      console.log("Enter a Course");
      axios
        .post("http://localhost:3000/courses.json", this.newCoursesParams)
        .then((response) => {
          console.log("course entered", response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
<template>
  <div class="courses-new">
    <form v-on:submit.prevent="createCourse()">
      <h1>Enter a course</h1>
      <div>
        <div class="course-group">
          Semester:
          <input type="text" v-model="newCoursesParams.semester_taken" />
        </div>
        <div class="course-group">
          Course name:
          <input type="text" v-model="newCoursesParams.name" />
        </div>
        <div class="course-group">
          Grade:
          <input type="text" v-model="newCoursesParams.grade" />
        </div>
        <div class="course-group">
          Credits:
          <select class="custom-select-sm" v-model="newCoursesParams.credits">
            <option selected>credits</option>
            <option>0.5</option>
            <option>1</option>
          </select>
        </div>
        <div class="course-group">
          Level:
          <select class="custom-select-sm" v-model="newCoursesParams.level">
            <option selected>levels</option>
            <option>traditional</option>
            <option>honors</option>
            <option>AP</option>
          </select>
        </div>
      </div>
      <br />
      <input type="submit" value="Create Course" />
    </form>
  </div>
</template>
