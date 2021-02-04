<template>
  <div class="card">
    <h4>№{{ index + 1 }}</h4>
    <ul style="">
      <li>Фамилия: {{ employee.surName }}</li>
      <li>Имя: {{ employee.firsthName }}</li>
      <li v-if="employee.middleName">Отчество: {{ employee.middleName }}</li>
      <li v-if="employee.middleName">Дата рождения: {{ employee.birthDay }}</li>
      <li v-if="employee.gender">Пол: {{ employee.gender }}</li>
      <li>Должность: {{ employee.position }}</li>
      <li v-if="employee.skills.length">
        Навыки:
        <div v-for="skill of employee.skills" :key="skill">{{ skill }}</div>
      </li>
      <li>Телефон: {{ employee.phone }}</li>
      <li v-if="employee.sendSms">СМС: Отправлять</li>
      <li v-else>СМС: Не отправлять</li>
      <li v-if="employee.index">Индекс: {{ employee.index }}</li>
      <li v-if="employee.country">Страна: {{ employee.country }}</li>
      <li v-if="employee.region">Область: {{ employee.region }}</li>
      <li>Город: {{ employee.city }}</li>
      <li v-if="employee.street">Улица: {{ employee.street }}</li>
      <li v-if="employee.house">Дом: {{ employee.house }}</li>
      <li>Документ: {{ employee.documentType }}</li>
      <li v-if="employee.series">Серия: {{ employee.series }}</li>
      <li v-if="employee.number">Номер: {{ employee.number }}</li>
      <li v-if="employee.issued">Выдал: {{ employee.issued }}</li>
      <li v-if="employee.dateIssued">Дата выдачи: {{ employee.dateIssued }}</li>
      <div class="button-wrapper">
        <button class="button" @click="$emit('removeImployee', employee._id)">
          Удалить сотрудника
        </button>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["employee", "index"],
  data: () => ({}),
};
</script>

<style scoped lang="scss">
.card {
  border-radius: 5px;
  box-shadow: 0 0 10px rgb(0 0 0 / 30%);
  padding: 15px;
  margin: 15px;
  width: 100%;

  ul {
    padding: 5px;
    list-style-type: none;
    text-align: left;
    margin: 0;

    li {
      padding: 5px;
      border-bottom: 1px solid grey;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }
  .button-wrapper {
    margin-top: 25px;

    .button {
      background: #109cf1;
      border-radius: 10px;
      height: 50px;
      font-size: 15px;
      color: #ffffff;
      border: none;
      width: 100%;
      outline: none;
    }
  }
}
</style>
