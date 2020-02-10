<template>
  <b-container fluid>
    <b-card>
      <b-container>
        <b-row>
          <b-col>
            <b-row>
              <b-col class="d-flex flex-row align-items-center">Course:
                <b-form-input class="ml-2" v-model="course" placeholder="Enter Course"></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-2">
              <button type="button" @click.prevent="addCourse" class="btn btn-primary">add</button>
            </b-row>
          </b-col>
          <b-col>
            <b-row>
              <b-col class="d-flex flex-row align-items-center">University:
                <b-form-input class="ml-2" v-model="Uni" placeholder="Enter Uni"></b-form-input>
              </b-col>
            </b-row>
          </b-col>
          <b-col>
            <b-row>
              <b-col class="d-flex flex-row align-items-center">Faculty:
                <b-form-select class="ml-2" v-model="selecprof" :options="professors"></b-form-select>
              </b-col>
            </b-row>
          </b-col>
        </b-row>
      </b-container>
    </b-card>
    <div class="border-top my-3"></div>

    <!--Render Created rows-->
    <b-card class="mt-1" v-for="(row, key) in rows" :key="key">
      <b-container>
        <b-row>
          <b-col>
            <b-row>
              <b-col class="d-flex flex-row align-items-center">Course:
                <b-form-input class="ml-2" v-model="row.course" :placeholder="row.course"></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-2">
              <button
                type="button"
                @click.prevent="removeCourse(key)"
                class="btn btn-danger"
              >remove course</button>
            </b-row>
          </b-col>
          <b-col>
            <b-row>
              <b-col>
                <b-row>
                  <b-col class="d-flex flex-row align-items-center">University:
                    <b-form-input class="ml-2" v-model="row.uniInput" placeholder="Enter Uni"/>
                  </b-col>
                </b-row>
                <b-row class="mt-2">
                  <button
                    type="button"
                    @click.prevent="addUniversity(key,row.uniInput)"
                    class="btn btn-primary"
                  >add Uni</button>
                </b-row>
                <b-row v-for="(uni,k) in row.universities" :key="k" class="mt-2 d-flex">
                  <b-col>{{uni.name}}</b-col>
                  <b-col>
                    <button
                      type="button"
                      @click.prevent="removeUniversity(key,k)"
                      class="ml-2 btn btn-danger"
                    >RM</button>
                  </b-col>
                </b-row>
              </b-col>
            </b-row>
          </b-col>
          <b-col>
            <b-row>
              <b-col class="d-flex flex-row align-items-center">Faculty:
                <b-form-select class="ml-2" v-model="selecprof" :options="professors"></b-form-select>
              </b-col>
            </b-row>
          </b-col>
        </b-row>
      </b-container>
    </b-card>
  </b-container>
</template>

<script>
export default {
  name: "course",
  components: {},

  data() {
    return {
      rows: [],
      course: "",
      Uni: "",
      selecprof: "F1",
      professors: [
        { value: "F1", text: "F1" },
        { value: "F2", text: "F2" },
        { value: "F3", text: "F3" }
      ]
    };
  },

  methods: {
    addUniversity(index) {
      this.rows[index].universities.push({ name: this.rows[index].uniInput });
      this.rows[index].uniInput = "";
    },

    removeUniversity(rowkey, unikey) {
      console.log();
      this.rows[rowkey].universities.splice(unikey, 1);
    },

    addCourse() {
      let Uni = { name: this.Uni };
      this.rows.push({
        course: this.course,
        uniInput: "",
        universities: [Uni],
        selecprof: this.selecprof
      });
      //reset
      this.Uni = "";
      this.course = "";
      this.selecprof = "F1";
    },

    removeCourse(index) {
      this.rows.splice(index, 2);
    }
  }
};
</script>