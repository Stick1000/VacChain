<template>
  <div class="columns is-centered">
    <div class="column is-three-quarters">
      <div class="columns fields is-left is-horizontal">
        <div class="column is-4 field-body">
          <div class="box">
            <div class="columns is-centered">
              <div class="column">
                <span class="icon is-large fa-5x mt-6 ml-6">
                  <FontAwesomeIcon icon="users" />
                </span>
              </div>
              <div class="column">
                <p class="title mt-5 mb-2">{{ vaccinatedIndividuals }}</p>
                <p class="label mb-0">Vaccinated</p>
                <p class="label mt-0 mb-0">Individuals</p>
                <p class="help mt-0 mb-2">{{ dateTimeNow() }}</p>
              </div>
            </div>
          </div>
        </div>

        <div class="column is-3 field-body">
          <div class="box">
            <div class="label has-text-centered">
              <span class="icon is-large fa-4x mt-3">
                <FontAwesomeIcon icon="calendar" />
              </span>
            </div>
            <p class="title has-text-centered mb-0">{{ dailyVaccinations }}</p>
            <p class="label has-text-centered">Daily Vaccinations</p>
          </div>
        </div>
      </div>

      <div class="box">
        <p class="title">Previous Days</p>
        <div>
          <img src="../assets/dummyChart.svg" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  methods: {
    dateTimeNow() {
      const current = new Date();
      return (
        current.getMonth() +
        1 +
        '-' +
        current.getDate() +
        '-' +
        current.getFullYear() +
        ' ' +
        (current.getHours() + ':' + current.getMinutes())
      );
    }
  },
  data() {
    return {
      vaccinatedIndividuals: 0,
      dailyVaccinations: 0
    };
  },
  created() {
    axios
      .post('http://localhost:5000/countEntries', {
        filter: { vaccine_info: { $gt: 0 } }
      })
      .then(response => {
        this.vaccinatedIndividuals = response.data;
      });

    axios
      .post('http://localhost:5000/countEntries', {
        filter: {
          $where: function () {
            const today = new Date(); //
            today.setHours(0, 0, 0, 0);
            return this._id.getTimestamp() >= today;
          }
        }
      })
      .then(response => {
        this.dailyVaccinations = response.data;
      });
  }
};
</script>

<style>
</style>