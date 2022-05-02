<template>
  <div class="part">
    <h4>寄送地址</h4>
    <div class="form-row-wrap d-flex justify-content-between">
      <div class="form-row d-flex flex-column w-20">
        <label for="">稱謂</label>
        <div class="select-wrapper">
          <select class="w-100" name="" id="" required>
            <option value="female">女士</option>
            <option value="male">男士</option>
          </select>
        </div>
      </div>
      <div class="form-row d-flex flex-column w-70">
        <label for="">姓名</label>
        <input type="text" name="" id="" placeholder="請輸入姓名" />
      </div>
    </div>
    <div class="form-row-wrap d-flex justify-content-between">
      <div class="form-row d-flex flex-column w-45 s-100">
        <label for="">電話</label>
        <input type="tel" name="" id="" placeholder="請輸入行動電話" />
      </div>
      <div class="form-row d-flex flex-column w-45 s-100">
        <label for="">Email</label>
        <input type="mail" name="" id="" placeholder="請輸入電子郵件" />
      </div>
    </div>
    <div class="form-row-wrap d-flex justify-content-between">
      <div class="form-row d-flex flex-column w-20 s-100">
        <label for="">縣市</label>
        <div class="select-wrapper">
          <select class="w-100" name="" id="" required>
            <option value="" disabled selected>請選擇縣市</option>
            <option value="TAIPEI">台北市</option>
            <option value="KEELUNG">基隆市</option>
          </select>
        </div>
      </div>
      <div class="form-row d-flex flex-column w-70 s-100">
        <label for="">地址</label>
        <input type="text" name="" id="" placeholder="請輸入地址" />
      </div>
    </div>
  </div>
</template>