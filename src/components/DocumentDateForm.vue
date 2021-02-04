<template>
  <form class="form" @submit.prevent="submitHandler">
    <h3 class="card-title">Создание нового сотрудника</h3>
    <h5>Документ</h5>
    <div class="card-content">
      <div class="select-field">
        <div>
          <select v-model.trim="documentType">
            <option value="null" selected hidden disabled>
              Выберите тип документа*
            </option>
            <option value="Паспорт">Паспорт</option>
            <option value="Свидетельство о рождении">
              Свидетельство о рождении
            </option>
            <option value="Вод. удостоверение">Вод. удостоверение</option>
          </select>
        </div>
        <small
          class="invalid"
          v-if="$v.documentType.$dirty && !$v.documentType.$model"
          >Поле тип документа не должно быть пустым</small
        >
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="series" placeholder="Серия" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="number" placeholder="Номер" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="issued" placeholder="Кем выдан" type="text" />
        </div>
      </div>
    </div>
    <div class="input-field">
      <div>
        <input
          placeholder="Когда выдан*"
          v-model.trim="dateIssued"
          onfocus=" (this.type='date')"
        />
      </div>

      <small
        class="invalid"
        v-if="$v.dateIssued.$dirty && !$v.dateIssued.required"
        >Поле дата выдачи не должно быть пустым</small
      >
    </div>
    <div class="button-wrapper">
      <button class="button" type="submit">Продолжить</button>
    </div>
  </form>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
  data: () => ({
    documentType: null,
    series: "",
    number: "",
    issued: "",
    dateIssued: "",
  }),
  validations: {
    documentType: { required },
    series: {},
    number: {},
    issued: {},
    dateIssued: { required },
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      const formData = {
        documentType: this.documentType,
        series: this.series,
        number: this.number,
        issued: this.issued,
        dateIssued: this.dateIssued,
      };

      this.$emit("changeCurrentForm", {
        page: "Basic-form",
        data: formData,
      });
    },
  },
};
</script>

<style scoped lang="scss">
.form {
  overflow: auto;
    height: 100%;
  h3 {
    margin: 30px;
  }
  .button-wrapper {
    margin: 5px;
    margin-bottom: 15px;
    .button {
      background: #109cf1;
      border-radius: 10px;
      height: 50px;
      font-size: 15px;
      color: #ffffff;
      border: none;
      width: 80%;
      outline: none;
    }
  }
  .select-field {
    padding: 6px;
    margin: 15px 0;
    height: 50px;
    select {
      width: 80%;
      border: 1px solid grey;
      outline: none;
      padding: 10px;
      border-radius: 4px;
      option {
        padding: 2px 0;
      }
    }
    .invalid {
      color: red;
    }
  }
  .input-field {
    padding: 5px;
    margin: 15px;
    height: 50px;
    flex-direction: column;
    display: flex;

    input {
      padding: 10px;
      border-radius: 4px;
      border: 1px solid grey;
      width: 80%;
      outline: none;
    }
    .invalid {
      color: red;
    }
  }
}
</style>
