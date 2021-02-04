<template>
  <form class="form" @submit.prevent="submitHandler">
    <h3>Создание нового сотрудника</h3>
    <h5>Основные данные</h5>
    <div>
      <div class="input-field">
        <div>
          <input placeholder="Фамилия*" v-model.trim="surName" type="text" />
        </div>

        <small class="invalid" v-if="$v.surName.$dirty && !$v.surName.required"
          >Поле фамилия не должно быть пустым</small
        >
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="firsthName" placeholder="Имя*" type="text" />
        </div>
        <small
          class="invalid"
          v-if="$v.firsthName.$dirty && !$v.firsthName.required"
          >Поле имя не должно быть пустым</small
        >
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="middleName" placeholder="Отчество" type="text" />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input
            v-model.trim="birthDay"
            placeholder="День рождения"
            onfocus=" (this.type='date')"
          />
        </div>
      </div>
      <div class="input-field">
        <div>
          <input v-model.trim="gender" placeholder="Пол" type="text" />
        </div>
      </div>
      <div class="select-field">
        <div>
          <select v-model.trim="position">
            <option value="null" selected hidden disabled>
              Выберите должность*
            </option>
            <option value="Frontend">Frontend</option>
            <option value="Backend">Backend</option>
            <option value="HR">HR</option>
            <option value="SEO">SEO</option>
            <option value="Manager">Manager</option>
            <option value="Другое">Другое</option>
          </select>
        </div>
        <small class="invalid" v-if="$v.position.$dirty && !$v.position.$model"
          >Поле должность не должно быть пустым</small
        >
      </div>
      <div v-if="$v.position.$model === 'Другое'" class="input-field">
        <div>
          <input
            v-model.trim="other"
            placeholder="Введите название должности*"
            type="text"
          />
        </div>
        <small class="invalid" v-if="$v.other.$dirty && !$v.other.requiredIf"
          >Поле должность не должно быть пустым</small
        >
      </div>

      <div style="height: 70px" class="select-field">
        <div>
          <select style="height: 70px" size="1" v-model.trim="skills" multiple>
            <option disabled>Выберите навыки</option>
            <option value="Навык-1">Навык-1</option>
            <option value="Навык-2">Навык-2</option>
            <option value="Навык-3">Навык-3</option>
            <option value="Навык-4">Навык-4</option>
            <option value="Навык-5">Навык-5</option>
          </select>
        </div>
      </div>
      <div class="input-field">
        <div>
          <input
            v-model.trim="phone"
            :class="{
              invalid:
                ($v.phone.$dirty && !$v.phone.required) ||
                ($v.phone.$dirty && !$v.phone.minLength),
            }"
            placeholder="Телефон*"
            type="text"
          />
        </div>
        <small class="invalid" v-if="$v.phone.$dirty && !$v.phone.required"
          >Поле телефон не должно быть пустым</small
        >
        <small
          class="invalid"
          v-if="$v.phone.$dirty && !$v.phone.isCorrectPhone && $v.phone.$model"
          >Поле телефон должно соответствовать образцу: 79999999999</small
        >
        <small
          class="invalid"
          v-else-if="$v.phone.$dirty && !$v.phone.maxLength && $v.phone.$model"
          >Поле Телефон не должно превышать 11 знаков</small
        >
      </div>
      <div class="checkbox-field">
        <label class="container"
          >Отправлять смс
          <input v-model.trim="sendSms" type="checkbox" />
          <span class="checkmark"></span>
        </label>
      </div>
    </div>
    <div class="button-wrapper">
      <button class="button" type="submit">Продолжить</button>
    </div>
  </form>
</template>

<script>
import { required, maxLength, requiredIf } from "vuelidate/lib/validators";
export default {
  data: () => ({
    surName: "",
    firsthName: "",
    middleName: "",
    birthDay: "",
    phone: "",
    gender: "",
    position: null,
    other: "",
    skills: [],
    sendSms: false,
  }),
  validations: {
    surName: { required },
    firsthName: { required },
    middleName: {},
    birthDay: {},
    gender: {},
    position: { required },
    other: {
      requiredIf: requiredIf(function () {
        return this.position === "Другое";
      }),
    },
    skills: {},
    phone: {
      required,
      maxLength: maxLength(11),
      isCorrectPhone(phone) {
        const regex = /7\(?([0-9]{3})\)?([ .-]?)([0-9]{3})\2([0-9]{4})/;
        return regex.test(phone);
      },
    },
    sendSms: {},
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      const formData = {
        surName: this.surName,
        firsthName: this.firsthName,
        middleName: this.middleName,
        birthDay: this.birthDay,
        gender: this.gender,
        position: this.position,
        other: this.other,
        skills: this.skills,
        phone: this.phone,
        sendSms: this.sendSms,
      };

      this.$emit("changeCurrentForm", {
        page: "Addres-form",
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
  .checkbox-field {
    padding: 5px;
    margin: 15px;
    display: flex;
    justify-content: center;

    .container {
      display: block;
      position: relative;
      padding-left: 35px;
      margin-bottom: 12px;
      cursor: pointer;
      font-size: 22px;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;

      .checkmark:after {
        content: "";
        position: absolute;
        display: none;
      }

      input:checked ~ .checkmark {
        background-color: #2196f3;
      }

      .checkmark {
        position: absolute;
        top: 0;
        left: 0;
        height: 25px;
        width: 25px;
        background-color: #eee;
      }

      input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
        height: 0;
        width: 0;
      }

      input:checked ~ .checkmark:after {
        display: block;
      }

      .checkmark:after {
        left: 9px;
        top: 5px;
        width: 5px;
        height: 10px;
        border: solid white;
        border-width: 0 3px 3px 0;
        -webkit-transform: rotate(45deg);
        -ms-transform: rotate(45deg);
        transform: rotate(45deg);
      }
    }

    .container:hover input ~ .checkmark {
      background-color: #ccc;
    }
  }
  .select-field {
    padding: 6px;
    margin: 15px 0;
    height: 40px;

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
