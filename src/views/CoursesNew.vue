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
        .post("http://localhost:3000/courses", this.newCoursesParams)
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
          <input type="text" v-model="newCoursesParams.credits" />
        </div>
        <div class="course-group">
          Level:
          <input type="text" v-model="newCoursesParams.level" />
        </div>
        <div class="course-group">
          user_id:
          <input type="text" v-model="newCoursesParams.user_id" />
        </div>
      </div>
      <input type="submit" value="Create Course" />
    </form>
  </div>
</template>
