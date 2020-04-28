<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <span><i class="fas fa-chart-line"></i></span>انشاء زبون جديد
      </div>
      <div class="col-md-6">
        <div class="back">
          <span><i class="fas fa-arrow-left"></i></span>الرجوع
        </div>
      </div>
    </div>

    <hr />
    <ul class="nav nav-tabs nav-fill" id="myTab" role="tablist">
      <li class="nav-item">
        <a
          class="nav-link active "
          data-toggle="tab"
          href="#"
          aria-selected="true"
          ><span><i class="far fa-user-circle"></i></span>البيانات الشخصية</a
        >
      </li>
      <li class="nav-item">
        <a class="nav-link " data-toggle="tab" href="#" aria-selected="false"
          ><span><i class="fas fa-envelope"></i></span>بيانات الاتصال</a
        >
      </li>
      <li class="nav-item">
        <a class="nav-link " data-toggle="tab" href="#" aria-selected="false">
          <span><i class="fas fa-file-invoice-dollar"></i></span>البيانات
          المالية</a
        >
      </li>
      <li class="nav-item">
        <a class="nav-link " data-toggle="tab" href="#" aria-selected="false"
          ><span><i class="fas fa-map-marked-alt"></i></span>البيانات العامة</a
        >
      </li>
    </ul>
    <ValidationObserver v-slot="{ handleSubmit, reset }">
      <form @submit.prevent="handleSubmit(onSubmit)" @reset.prevent="reset">
        <div class="form-group row">
          <label for="inputName" class="col-sm-2 col-form-label">الاسم</label>
          <div class="col-sm-5">
            <input type="text" class="form-control" id="inputName" />
          </div>
          <div class="col-sm-2">
            <ValidationProvider
              rules="required"
              :bails="false"
              v-slot="{ errors }"
              name="الاسم"
            >
              <select class="form-control" v-model="name">
                <option> الانجليزية</option>
                <option>العربية</option>
              </select>
              <ul class="error">
                <li v-for="error in errors" :key="error">{{ error }}</li>
              </ul>
            </ValidationProvider>
          </div>
          <div class="col-sm-1">
            <span><i class="fas fa-minus"></i></span>
          </div>
        </div>
        <div class="form-group row mx-auto " style="width: 200px;">
          <span><i class="fas fa-plus"></i></span>
        </div>

        <div class="form-group row">
          <label for="inputGroupType" class="col-sm-2 col-form-label"
            >نوع المجموعة</label
          >
          <div class="col-sm-8">
            <select class="form-control">
              <option> </option>
            </select>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputCode" class="col-sm-2 col-form-label">الكود </label>
          <div class="col-sm-8">
            <ValidationProvider
              rules="required"
              :bails="false"
              v-slot="{ errors }"
              name="الكود"
            >
              <input
                type="text"
                class="form-control"
                id="inputCode"
                placeholder="ادخل الكود"
                v-model="inputCode"
              />
              <ul class="error">
                <li v-for="error in errors" :key="error">{{ error }}</li>
              </ul>
            </ValidationProvider>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputNationality" class="col-sm-2 col-form-label"
            >الجنسية
          </label>
          <div class="col-sm-8">
            <select class="form-control">
              <option> افغانستان </option>
            </select>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputTaxNumber" class="col-sm-2 col-form-label"
            >الرقم الضريبي
          </label>
          <div class="col-sm-8">
            <ValidationProvider
              rules="required|numeric"
              :bails="false"
              v-slot="{ errors }"
              name="الرقم الضريبي"
            >
              <input
                type="text"
                class="form-control"
                id="inputTaxNumber"
                placeholder="ادخل الرقم الضريبي"
                v-model="inputTaxNumber"
              />

              <ul class="error">
                <li v-for="error in errors" :key="error">{{ error }}</li>
              </ul>
            </ValidationProvider>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputSalesPerson" class="col-sm-2 col-form-label">
            مندوب المبيعات</label
          >
          <div class="col-sm-8">
            <input
              type="text"
              class="form-control"
              id="inputSalesPerson"
              placeholder="ادخل مندوب المبيعات"
            />
          </div>
        </div>
        <div class="form-group row">
          <label for="inputVirtualCurrency" class="col-sm-2 col-form-label"
            >العملة الافتراضية</label
          >
          <div class="col-sm-8">
            <select class="form-control">
              <option> درهم اماراتي</option>
              <option>دولار امريكي</option>
            </select>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputGender" class="col-sm-2 col-form-label">
            الجنس</label
          >
          <div class="col-sm-8">
            <select class="form-control">
              <option> ذكر</option>
              <option>انثى </option>
            </select>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputStartDate" class="col-sm-2 col-form-label">
            تاريخ البداية</label
          >
          <div class="col-sm-8">
            <date-picker v-model="date" />
          </div>
        </div>
        <div class="form-group row">
          <button class="btn" style="border:1px solid #ccc" type="reset">
            اعادة تعيين
          </button>
          <button class="btn btn-primary" type="submit">ارسال</button>
        </div>
      </form>
    </ValidationObserver>
  </div>
</template>

<script>
import DatePicker from "v-calendar/lib/components/date-picker.umd";
//import Calendar from 'v-calendar/lib/components/calendar.umd'
export default {
  components: {
    // Calendar,
    DatePicker,
  },
  data() {
    return {
      date: new Date(),
      yourValue: null, // Jan 25th, 2018
      inputTaxNumber: 0,
      inputCode: "",
      name: "",
    };
  },
  methods: {
    onSubmit() {
      alert("Form has been submitted!");
    },
  },
};
</script>

<style>
.back {
  float: left;
}
.container {
  font-size: 15px;
  margin-top: 20px;
}
form {
  margin-top: 20px;
}
li {
  font-size: 15px;
  /* font-weight: bold; */
}
i {
  padding: 5px;
}
i.fas.fa-minus {
  border: 1px solid red;
  color: red;
  border-radius: 25px;
}
i.fas.fa-plus {
  border: 1px solid #2fd52f;
  color: #2fd52f;
  border-radius: 25px;
}
/* a.nav-link{
  color: black;
} */
/* .nav-background{
background-color: powderblue;
} */
.error {
  color: red;
}
</style>
