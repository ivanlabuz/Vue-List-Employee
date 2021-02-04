<template>
  <div class="main-wrapper">
    <div class="wrapper">
      <template v-if="isListPage">
        <ListEmployees
          v-on:changeCurrentPage="changeCurrentPage"
        />
      </template>
      <template v-else>
        <template v-if="currentForm === 'Basic-form'">
          <BasicDataForm v-on:changeCurrentForm="changeCurrentForm" />
        </template>
        <template v-if="currentForm === 'Addres-form'">
          <AddresDateForm v-on:changeCurrentForm="changeCurrentForm" />
        </template>
        <template v-if="currentForm === 'Document-form'">
          <DocumentDateForm v-on:changeCurrentForm="changeCurrentForm" />
        </template>
      </template>
    </div>
  </div>
</template>

<script>
import BasicDataForm from "@/components/BasicDataForm";
import DocumentDateForm from "@/components/DocumentDateForm";
import AddresDateForm from "@/components/AddresDateForm";
import ListEmployees from "@/components/ListEmployees";
export default {
  data: () => ({
    isListPage: true,
    currentForm: "Basic-form",
    newEmployee: {},
  }),
  components: {
    BasicDataForm,
    DocumentDateForm,
    AddresDateForm,
    ListEmployees,
  },
  methods: {
    changeCurrentForm({ page, data }) {
      this.newEmployee = {
        ...this.newEmployee,
        ...data,
        _id: new Date(),
      };
      this.currentForm = page;

      if (page === "Basic-form") {
        if (!localStorage.listEmployee) {
          localStorage.listEmployee = JSON.stringify([this.newEmployee]);
        } else {
          const currentLocalStorage = JSON.parse(localStorage.listEmployee);
          currentLocalStorage.push(this.newEmployee);
          localStorage.listEmployee = JSON.stringify(currentLocalStorage);
        }
        this.isListPage = true;
      }
    },

    changeCurrentPage() {
      this.isListPage = false;
    },
  },
};
</script>

<style scoped lang="scss">
.main-wrapper {
  display: flex;
  align-items: center;
  height: 100vh;
  justify-content: center;
  
  .wrapper {
    width: 80%;
    border-radius: 5px;
    text-align: center;
    box-shadow: 0 0 10px rgb(0 0 0 / 30%);
    height: 85%;
    position: relative;
  }
}
</style>
