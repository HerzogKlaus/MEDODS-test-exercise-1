<template>
  <div class="wrapper">
    <div class="success" v-if="success">
      Клиент успешно создан
    </div>
    <form class="form-block" method="POST" @submit.prevent="onSubmit()">
      <h1 class="form-block__title">Форма создания клиента</h1>
      <div class="form-block__item">
        <label for="surname">Фамилия<sup class="required-mark">*</sup></label>
        <input
          class="form-block__item-field"
          :class="{ 'is-invalid': $v.surname.$error }"
          type="text"
          name="surname"
          id="surname"
          @blur="$v.surname.$touch()"
          v-model="surname"
        />
        <pre class="invalid-feedback" v-if="$v.surname.$error">
Поле не заполнено или заполнено некорректно</pre
        >
      </div>
      <div class="form-block__item">
        <label for="name">Имя<sup class="required-mark">*</sup></label>
        <input
          class="form-block__item-field"
          :class="{ 'is-invalid': $v.name.$error }"
          type="text"
          name="name"
          id="name"
          @blur="$v.name.$touch()"
          v-model="name"
        />
        <pre class="invalid-feedback" v-if="$v.name.$error">
Поле не заполнено или заполнено некорректно</pre
        >
      </div>
      <div class="form-block__item">
        <label for="middlename">Отчество</label>
        <input
          class="form-block__item-field"
          :class="{ 'is-invalid': $v.middlename.$error }"
          type="text"
          name="middlename"
          id="middlename"
          @blur="$v.middlename.$touch()"
          v-model="middlename"
        />
        <pre class="invalid-feedback" v-if="$v.middlename.$error">
Поле заполнено некорректно</pre
        >
      </div>
      <div class="form-block__item">
        <label for="birth-date"
          >Дата рождения<sup class="required-mark">*</sup></label
        >
        <input
          class="form-block__item-field"
          :class="{ 'is-invalid': $v.dateBirth.$error }"
          type="date"
          name="birth-date"
          id="birth-date"
          @blur="$v.dateBirth.$touch()"
          v-model="birthDate"
        />
        <pre class="invalid-feedback" v-if="$v.dateBirth.$error">
Поле не заполнено или заполнено некорректно</pre
        >
      </div>
      <div class="form-block__item">
        <label for="phone"
          >Номер телефона<sup class="required-mark">*</sup></label
        >
        <input
          class="form-block__item-field"
          :class="{ 'is-invalid': $v.phone.$error }"
          type="tel"
          name="phone"
          id="phone"
          @blur="$v.phone.$touch()"
          v-model="phone"
        />
        <pre class="invalid-feedback" v-if="$v.phone.$error">
Поле не заполнено или заполнено некорректно</pre
        >
      </div>
      <div class="form-block__item form-block__item--gender">
        <div class="form-block__item-title">Пол</div>
        <div class="form-block__item-gender">
          <div class="form-block__item-gender-item">
            <input
              class="form-block__item-field form-block__item-field--radio"
              type="radio"
              name="gender"
              value="male"
              id="gender-male"
            />
            <label for="gender-male">Мужской</label>
          </div>
          <div class="form-block__item-gender-item">
            <input
              class="form-block__item-field form-block__item-field--radio"
              type="radio"
              name="gender"
              value="female"
              id="gender-female"
            />
            <label for="gender-female">Женский</label>
          </div>
        </div>
      </div>
      <div class="form-block__item">
        <label for="client-group"
          >Группа клиентов<sup class="required-mark">*</sup></label
        >
        <select
          class="form-block__item-field"
          :class="{ 'is-invalid': $v.clientGroup.$error }"
          name="client-group"
          id="client-group"
          @blur="$v.clientGroup.$touch()"
          v-model="clientGroup"
        >
          <option v-for="group in clientGroups" :key="group" :value="group">
            {{ group }}
          </option>
        </select>
        <pre class="invalid-feedback" v-if="$v.clientGroup.$error">
Поле не заполнено или заполнено некорректно</pre
        >
      </div>
      <div class="form-block__item">
        <label for="doctor">Лечащий врач</label>
        <select class="form-block__item-field" name="doctor" id="doctor">
          <option v-for="doctor in doctors" :key="doctor" :value="doctor">
            {{ doctor }}
          </option>
        </select>
      </div>
      <div class="form-block__item">
        <label for="sms">Не отправлять СМС</label>
        <input
          class="form-block__item-field form-block__item-field--check"
          type="checkbox"
          name="SMS"
          value="Не отправлять"
          id="sms"
        />
      </div>

      <div class="form-block__item-section">
        <div class="form-block__item-section-title">Адрес</div>
        <div class="form-block__item">
          <label for="index">Индекс</label>
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.index.$error }"
            type="text"
            name="index"
            id="index"
            @blur="$v.index.$touch()"
            v-model="index"
          />
          <pre class="invalid-feedback" v-if="$v.index.$error">
Поле заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="country">Страна</label>
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.index.$error }"
            type="text"
            name="country"
            id="country"
            @blur="$v.country.$touch()"
            v-model="country"
          />
          <pre class="invalid-feedback" v-if="$v.country.$error">
Поле заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="region">Область</label>
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.region.$error }"
            type="text"
            name="region"
            id="region"
            @blur="$v.region.$touch()"
            v-model="region"
          />
          <pre class="invalid-feedback" v-if="$v.region.$error">
Поле заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="city">Город<sup class="required-mark">*</sup></label>
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.city.$error }"
            type="text"
            name="city"
            id="city"
            @blur="$v.city.$touch()"
            v-model="city"
          />
          <pre class="invalid-feedback" v-if="$v.city.$error">
Поле не заполнено или заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="street">Улица</label>
          <input
            class="form-block__item-field"
            type="text"
            name="street"
            id="street"
          />
        </div>
        <div class="form-block__item">
          <label for="house">Дом</label>
          <input
            class="form-block__item-field"
            type="text"
            name="house"
            id="house"
          />
        </div>
      </div>

      <div class="form-block__item-section">
        <div class="form-block__item-section-title">Паспорт</div>
        <div class="form-block__item">
          <label for="document-type"
            >Тип документа<sup class="required-mark">*</sup></label
          >
          <select
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.documentType.$error }"
            name="document-type"
            id="document-type"
            @blur="$v.documentType.$touch()"
            v-model="documentType"
          >
            <option v-for="type in documentTypes" :key="type" :value="type">
              {{ type }}
            </option>
          </select>
          <pre class="invalid-feedback" v-if="$v.documentType.$error">
Поле не заполнено или заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="series">Серия</label>
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.series.$error }"
            type="text"
            name="series"
            id="series"
            @blur="$v.series.$touch()"
            v-model="series"
          />
          <pre class="invalid-feedback" v-if="$v.series.$error">
Поле заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="number">Номер</label>
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.number.$error }"
            type="text"
            name="number"
            id="number"
            @blur="$v.number.$touch()"
            v-model="number"
          />
          <pre class="invalid-feedback" v-if="$v.number.$error">
Поле заполнено некорректно</pre
          >
        </div>
        <div class="form-block__item">
          <label for="issued-by">Кем выдан</label>
          <input
            class="form-block__item-field"
            type="text"
            name="issued-by"
            id="issued-by"
          />
        </div>
        <div class="form-block__item">
          <label for="issue-date"
            >Дата выдачи<sup class="required-mark">*</sup></label
          >
          <input
            class="form-block__item-field"
            :class="{ 'is-invalid': $v.dateIssue.$error }"
            type="date"
            name="issue-date"
            id="issue-date"
            @blur="$v.dateIssue.$touch()"
            v-model="issueDate"
          />
          <pre class="invalid-feedback" v-if="$v.dateIssue.$error">
Поле не заполнено или заполнено некорректно</pre
          >
        </div>
      </div>
      <button class="form-block__button" type="submit" :disabled="$v.$invalid">
        Отправить
      </button>
    </form>
  </div>
</template>

<script>
/*eslint-disable*/
import {
  required,
  minLength,
  maxLength,
  numeric,
  maxValue,
} from "vuelidate/lib/validators";
export default {
  data: () => ({
    surname: "",
    name: "",
    middlename: "",
    birthDate: "",
    phone: "7",
    clientGroup: "",
    index: "",
    country: "",
    region: "",
    city: "",
    documentType: "",
    series: "",
    number: "",
    issueDate: "",
    success: false,
    clientGroups: ["VIP", "Проблемные", "ОМС"],
    doctors: ["Иванов", "Захаров", "Чернышева"],
    documentTypes: [
      "Паспорт",
      "Свидетельство о рождении",
      "Водительское удостоверение",
    ],
  }),

  computed: {
    dateBirth() {
      return this.birthDate ? new Date(this.birthDate) : null;
    },
    dateIssue() {
      return this.issueDate ? new Date(this.issueDate) : null;
    },
  },

  methods: {
    onSubmit() {
      this.surname = "",
        this.name = "",
        this.middlename = "",
        this.birthDate = "",
        this.phone = "",
        this.clientGroup = "",
        this.index = "",
        this.country = "",
        this.region = "",
        this.city = "",
        this.documentType = "",
        this.series = "",
        this.number = "",
        this.issueDate = "",
        this.success = true
    },
  },

  validations: {
    surname: {
      required,
      letterOnly(text) {
        return /^[а-яА-ЯёЁ\s]+$/.test(text);
      },
    },
    name: {
      required,
      letterOnly(text) {
        return /^[а-яА-ЯёЁ\s]+$/.test(text);
      },
    },
    middlename: {
      letterOnly(text) {
        return /^[а-яА-ЯёЁ\s]+$/.test(text);
      },
    },
    dateBirth: {
      required,
      maxValue: maxValue(new Date().setDate(new Date().getDate() + 1)),
    },
    phone: {
      required,
      numeric,
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    clientGroup: {
      required,
    },
    index: {
      numeric,
    },
    country: {
      letterOnly(text) {
        return /^[а-яА-ЯёЁ\s]+$/.test(text);
      },
    },
    region: {
      letterOnly(text) {
        return /^[а-яА-ЯёЁ\s]+$/.test(text);
      },
    },
    city: {
      required,
      letterOnly(text) {
        return /^[а-яА-ЯёЁ\s]+$/.test(text);
      },
    },
    documentType: {
      required,
    },
    series: {
      numeric,
    },
    number: {
      numeric,
    },
    dateIssue: {
      required,
      maxValue: maxValue(new Date().setDate(new Date().getDate() + 1)),
    },
  },
};
</script>
