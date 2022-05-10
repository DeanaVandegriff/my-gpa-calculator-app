<script>
import axios from "axios";
export default {
  data: function () {
    return {
      course: {},
      editCoursesParams: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/courses/" + this.$route.params.id + ".json").then((response) => {
      console.log(response.data);
      this.course = response.data;
    });
  },
  methods: {
    updateCourse: function () {
      console.log("Update a course!");
      axios.patch("http://localhost3000/courses/" + this.$route.params.id + ".json", this.course).then((response) => {
        console.log("Success", response.data);
        this.$router.push("/courses");
      });
    },
  },
};
</script>

<template>
  <div class="courses-edit">
    <form v-on:submit.prevent="updateCourse()">
      <h1>Update a Course</h1>
      <div>
        <div class="form-group">
          Name:
          <input type="text" v-model="course.name" />
        </div>
        <div class="form-group">
          Grade:
          <input type="text" v-model="course.grade" />
        </div>
        <div class="form-group">
          Credits:
          <input type="text" v-model="course.credits" />
        </div>
        <div class="form-group">
          Semester:
          <input type="text" v-model="course.semester_taken" />
        </div>
      </div>
      <input type="submit" value="Update" />
    </form>
    <a href="`/courses/${course.id}`">Back to all Courses</a>
  </div>
</template>
