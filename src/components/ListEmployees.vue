<template>
  <div class="main-wrapper-list">
    <h3>Список сотрудников</h3>
    <div class="wrapper-list">
      <div no-list v-if="loading" class="no-list">
        <Loader />
      </div>
      <div class="list" v-else-if="listEmployees.length">
        <EmploeCard
          v-for="(employee, i) of listEmployees"
          v-bind:employee="employee"
          v-bind:index="i"
          :key="employee._id"
          v-on:removeImployee="removeImployee"
        />
      </div>
      <div class="no-list" v-else>
        Сотрудники отсутствуют. Но вы всегда можете создать нового.
      </div>
      <div class="button-wrapper">
        <button class="button" v-on:click="$emit('changeCurrentPage')">
          Создать нового сотрудника
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import EmploeCard from "@/components/EmploeCard";
import Loader from "@/components/Loader";
export default {
  data: () => ({
    loading: true,
    listEmployees: [],
  }),
  mounted() {
    setTimeout(() => {
      if (localStorage.listEmployee) {
        this.listEmployees = JSON.parse(localStorage.listEmployee);
      }
      this.loading = false;
    }, 1000);
  },
  components: {
    EmploeCard,
    Loader,
  },
  methods: {
    removeImployee(id) {
      this.listEmployees = this.listEmployees.filter(
        (employee) => employee._id !== id
      );
      localStorage.listEmployee = JSON.stringify(this.listEmployees);
    },
  },
};
</script>

<style scoped lang="scss">
.main-wrapper-list {
  height: 80%;

  h1 {
    margin-top: 35px;
  }

  .button-wrapper {
    margin: 14px;
    position: absolute;
    bottom: 0;
    width: 50%;

    .button {
      background: #109cf1;
      border-radius: 10px;
      height: 50px;
      font-size: 15px;
      color: #ffffff;
      border: none;
      outline: none;
    }
  }

  .wrapper-list {
    display: flex;
    justify-content: center;
    overflow: auto;
    height: 103%;

    .list {
      align-items: center;
      display: flex;
      flex-direction: column;
      width: 80%;
    }
    .no-list {
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }

  @media screen and (max-width: 426px) {
    overflow: hidden;
    height: 84%;
    .wrapper-list {
      height: calc(100% - 56px);
    }
  }
}
</style>