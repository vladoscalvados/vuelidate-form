<template>
  <div class="container">
    <div class="card col-12">
      <div class="card-header">Регистрация</div>
      <form class="form" id="signup-form" @submit.prevent="submitForm">
        <div class="form-group"></div>
        <label>Фамилия <span class="text-danger">*</span></label>
        <input class="form-control"
               :class="$v.form.lastname.$error ? 'is-invalid' : '' "
               type="text"
               v-model="form.lastname"
        />
        <span v-if="$v.form.lastname.$dirty && !$v.form.lastname.required "
              class="invalid-feedback">Поле не может быть пустым</span>

        <div class="form-group"></div>
        <label>Имя<span class="text-danger">*</span></label>
        <input class="form-control"
               :class="$v.form.name.$error ? 'is-invalid' : '' "
               type="text"
               v-model="form.name"
        />
        <span v-if="$v.form.name.$dirty && !$v.form.name.required "
              class="invalid-feedback">Поле не может быть пустым</span>

        <div class="form-group"></div>
        <label>Отчество<span class="text-danger">*</span></label>
        <input class="form-control"
               :class="$v.form.patronymic.$error ? 'is-invalid' : '' "
               type="text"
               v-model="form.patronymic"
        />
        <span v-if="$v.form.patronymic.$dirty && !$v.form.patronymic.required "
              class="invalid-feedback">Поле не может быть пустым</span>

        <div class="form-group"></div>
        <label>Номер телефона <span class="text-danger">*</span></label>
        <input class="form-control"
               :class="$v.form.phone.$error ? 'is-invalid' : '' "
               id="phone"
               type="number"
               v-model="form.phone"/>


        <span v-if="$v.form.phone.$dirty && !$v.form.phone.minLength "
              class="invalid-feedback">Номер должен быть не менее 10 цифр </span>

        <div class="form-group"></div>
        <label>Пол <span class="text-danger">*</span></label>

        <div class="flex">

          <div class="form-check">
            <input type="radio" class="form-check-input" name="exampleRadio" id="male" v-model="form.gender"
                   value="male"
            >
            <label class="form-check-label" for="male">
              Мужской
            </label>
          </div>

          <div class="form-check">
            <input type="radio" class="form-check-input" name="exampleRadio" id="female" v-model="form.gender"
                   value="female">
            <label class="form-check-label" for="female">
              Женский
            </label>
          </div>
        </div>


        <div class="form-group">
          <label for="clients">Группа клиентов <span class="text-danger">*</span></label>
          <select id="clients" class="form-control" v-model="form.client" multiple>
            <option v-for="(client,index) in form.clients" :key="index">{{ client.label }}</option>
          </select>
        </div>

        <div class="form-group">
          <label for="doctor">Лечащий врач <span class="text-danger">*</span></label>
          <select id="doctor" class="form-control" v-model="form.doctor">
            <option v-for="(doctor,index) in form.doctors" :key="index">{{ doctor.label }}</option>
          </select>
        </div>

        <div class="form-check">
          <input type="radio" class="form-check-input"
                 id="SMS"
                 v-model="form.agreeSendSms"
          >
          <label class="form-check-label">
            Не отправлять смс
          </label>
        </div>

        <div class="form-group"></div>
        <label>Индекс</label>
        <input class="form-control" type="number"/>

        <div class="form-group"></div>
        <label>Страна</label>
        <input class="form-control" type="text"/>

        <div class="form-group"></div>
        <label>Область</label>
        <input class="form-control" type="text"/>

        <div class="form-group"></div>
        <label>Город <span class="text-danger">*</span></label>
        <input class="form-control"
               :class="$v.form.city.$error ? 'is-invalid' : '' "
               type="text"
               v-model.trim="form.city"
        />
        <span v-if="$v.form.lastname.$dirty && !$v.form.city.required "
              class="invalid-feedback">Поле не может быть пустым</span>

        <div class="form-group"></div>
        <label>Улица</label>
        <input class="form-control" type="text"/>

        <div class="form-group"></div>
        <label>Дом</label>
        <input class="form-control" type="number"/>


        <div class="form-group">
          <label for="document">Тип документ<span class="text-danger">*</span></label>
          <select id="document" class="form-control" v-model="form.document">
            <option v-for="(document,index) in form.documents" :key="index">{{document.label }}</option>
          </select>
        </div>

        <div class="form-group"></div>
        <label>Серия</label>
        <input class="form-control" type="number"/>

        <div class="form-group"></div>
        <label>Номер</label>
        <input class="form-control" type="number"/>

        <div class="form-group"></div>
        <label>Кем выдан</label>
        <input class="form-control" type="text"/>

        <div class="form-group"></div>
        <label>Дата выдачи</label>
        <input class="form-control" type="number"/>

        <button class="btn btn-primary" type="submit">Создать</button>

      </form>
    </div>
  </div>
</template>

<script>

import {required, minLength} from 'vuelidate/lib/validators'


export default {
  data() {
    return {
      form:{


        name: '',
        lastname: '',
        patronymic: '',
        phone: '',
        gender:[''],
        client: [''],
        clients: [
          {
            label: 'VIP',
            value: 'vip'
          },
          {
            label: 'Проблемные',
            value: 'problem'
          },
          {
            label: 'OMC',
            value: 'omc'
          },
        ],
        doctor: '',
        doctors: [
          {
            label: 'Иванов',
            value: 'Ivanov'
          },
          {
            label: 'Захаров',
            value: 'Zaharov'
          },
          {
            label: 'Чернышева',
            value: 'Chernysheva'
          },
        ],
        agreeSendSms: false,
        city: '',
        document: '',
        documents: [
          {
            label: 'Паспорт',
            value: 'passport'
          },
          {
            label: 'Свидетельство о рождении',
            value: 'certificate'
          },
          {
            label: 'Водительские права',
            value: 'drive licence'
          },

        ],
      }
    }
  },
  validations: {
    form:{
      name: {required},
      lastname: {required},
      patronymic: {required},
      phone: { minLength: minLength(10)},
      gender: {required},
      city: {required},
    }


  },
  methods: {
    submitForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert('Валидация успешна')
      }
    }
  }


}


</script>


<style scoped>
.container {
  display: flex;
  flex-direction: column;
}

.card {
  background-color: rgb(255, 255, 240);
}

input {
  background-color: rgb(255, 250, 250);

}

.flex {
  display: flex;
  justify-content: center;
}
.form-group {
  margin: 10px 0 ;
}

.form-check{
  margin: 0 15px;
}

</style>