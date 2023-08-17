## Homework #3

## 1. Endpoint /login

Отправить запрос
`POST http://162.55.220.72:5005/login`

Body: form-data

### 1.1 Приходящий токен передать во все остальные запросы

Забираем токен из ответа и устанавливаем его в переменную окружения:
```
var respBody = pm.response.json();
var token = respBody.token;
pm.environment.set("my_token", token);
```
Далее в остальных запросах будем использовать переменную `{{my_token}}`

## 2. Endpoint /user_info

Отправить запрос
`POST http://162.55.220.72:5005/user_info`

Body: raw -> JSON

### 2.1 Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### ???2.2 Проверка структуры json в ответе



### 2.3 В ответе указаны коэффициенты умножения salary. Написать тесты по проверке правильности результата уммножения на коэффициент
```
var respBody = pm.response.json();

pm.test("Check that response salary*2 and response qa_salary_after_6_months are equal", function () {   
    pm.expect(respBody.person.u_name[1] * 2).to.eql(respBody.qa_salary_after_6_months);
});

pm.test("Check that response salary*2.9 and response qa_salary_after_12_months are equal", function () {   
    pm.expect(respBody.person.u_name[1] * 2.9).to.eql(respBody.qa_salary_after_12_months);
});

pm.test("Check that response salary*4 and response u_salary_1.5_year are equal", function () {   
    pm.expect(respBody.person.u_name[1] * 4).to.eql(respBody.person.u_salary_1_5_year);
});
```
### 2.4 Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user

Устанавливаем значение поля u_salary_1.5_year в качестве переменной окружения:

`pm.environment.set("new_salary", respBody.person.u_salary_1_5_year);`

## 3. Endpoint /new_data

Отправить запрос
`POST http://162.55.220.72:5005/new_data`

Body: form-data

### 3.1 Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### ???3.2 Проверка структуры json в ответе



### 3.3 В ответе указаны коэффициенты умножения salary. Написать тесты по проверке правильности результата уммножения на коэффициент
```
var respBody = pm.response.json();

pm.test("Check that response salary[0]*2 and response salary[1] are equal", function () {   
    pm.expect(respBody.salary[0] * 2).to.eql(+respBody.salary[1]);
});

pm.test("Check that response salary[0]*3 and response salary[2] are equal", function () {   
    pm.expect(respBody.salary[0] * 3).to.eql(+respBody.salary[2]);
});
```
### 3.4 Проверить, что 2-й элемент массива salary больше 1-го и 0-го
```
pm.test("Check that response salary[2] is greater than salary[1] and salary[0]", function () {   
    pm.expect(+respBody.salary[2]).to.be.gt(+respBody.salary[1]);
    pm.expect(+respBody.salary[2]).to.be.gt(respBody.salary[0]);
});
```

## 4. Endpoint /test_pet_info

Отправить запрос
`POST http://162.55.220.72:5005/test_pet_info`

Body: form-data

### 4.1 Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### ???4.2 Проверка структуры json в ответе


### 4.3 В ответе указаны коэффициенты умножения weight. Написать тесты по проверке правильности результата умножения на коэффициент
```
var respBody = pm.response.json();
var reqBody = request.data;

pm.test("Check that daily_food is equal to weight * 0.012", function () {   
    pm.expect(respBody.daily_food).to.eql(reqBody.weight * 0.012);
});

pm.test("Check that daily_sleep is equal to weight * 2.5", function () {   
    pm.expect(respBody.daily_sleep).to.eql(reqBody.weight * 2.5);
});
```

## 5. Endpoint /get_test_user

Отправить запрос
`POST http://162.55.220.72:5005/test_pet_info`

Body: form-data

Для поля `salary` значение забираем из переменной окружения, созданной в п.2.4

### 5.1 Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### ???5.2 Проверка структуры json в ответе

### 5.3 Проверить, что значение поля name равно значению переменной name из окружения
```
var respBody = pm.response.json();
var reqBody = request.data;
var name_env = pm.environment.get("name");

pm.test("Check that environment name and response name are equal", function () {   
    pm.expect(respBody.name).to.eql(name_env);
});
```
### 5.4 Проверить, что значение поля age в ответе соответствует отправленному в запросе значению поля age
```
pm.test("Check that request age and response age are equal", function () {   
    pm.expect(respBody.age).to.eql(reqBody.age);
});
```
