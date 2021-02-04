<template>
  <form class="form" @submit.prevent="submitHandler">
    <h3 class="card-title">Создание нового сотрудника</h3>
    <h5>Адрес</h5>
    <div class="card-content">
      <div class="input-field">
        <div>
          <input v-model.trim="index" placeholder="Индекс" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="country" placeholder="Страна" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="region" placeholder="Область" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="city" placeholder="Город*" type="text" />
        </div>
        <small class="invalid" v-if="$v.city.$dirty && !$v.city.required"
          >Поле город не должно быть пустым</small
        >
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="street" placeholder="Улица" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="house" placeholder="Дом" type="text" />
        </div>
      </div>
      <div>
        <div class="button-wrapper">
          <button class="button" type="submit">Продолжить</button>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
  data: () => ({
    index: "",
    country: "",
    region: "",
    city: "",
    street: "",
    house: "",
  }),
  validations: {
    index: {},
    country: {},
    region: {},
    city: { required },
    street: {},
    house: {},
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      const formData = {
        index: this.index,
        country: this.country,
        region: this.region,
        city: this.city,
        street: this.street,
        house: this.house,
      };
      this.$emit("changeCurrentForm", {
        page: "Document-form",
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
  .input-field {
    padding: 5px;
    margin: 15px;
    height: 40px;
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
