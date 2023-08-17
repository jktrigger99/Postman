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
### 2.2 Проверка структуры json в ответе

Составляем JSON Schema для нашего объекта:
```
var schema = {
    "type": "object",
    "properties": {
        "start_qa_salary": {
            "type": "integer"
        },
        "qa_salary_after_6_months": {
            "type": "integer"
        },
        "qa_salary_after_12_months": {
            "type": "number"
        },
        "person": {
            "type": "object",
            "properties": {
                "u_age": {
                    "type": "integer"
                },
                "u_salary_1_5_year": {
                    "type": "integer"
                },
                "u_name": {
                    "type": "array",
                    "items": [
                        { "type": "string" },
                        { "type": "integer" },
                        { "type": "integer" }
                    ]
                }
            },
            "required": ["u_age", "u_name", "u_salary_1_5_year"]           
        }
    },
    "required": ["start_qa_salary", "qa_salary_after_6_months", "qa_salary_after_12_months", "person"]
}
```
Проверяем структуру ответа с помощью tiny validator:
```
pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(respBody, schema)).to.be.true;
});
console.log(tv4.error);
```

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
### 3.2 Проверка структуры json в ответе

Составляем JSON Schema для нашего объекта:
```
var schema = {
    "type": "object",
    "properties": {
        "age": {
            "type": "integer"
        },
        "name": {
            "type": "string"
        },
        "salary": {
            "type": "array",
            "items": [
                { "type": "integer" },
                { "type": "string" },
                { "type": "string" }
            ]
        }
    },
    "required": ["age", "name", "salary"]
}
```
Проверяем структуру ответа с помощью tiny validator:
```
pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(respBody, schema)).to.be.true;
});
console.log(tv4.error);
```
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
### 4.2 Проверка структуры json в ответе

Составляем JSON Schema для нашего объекта:
```
var schema = {
    "type": "object",
    "properties": {
        "age": {
            "type": "integer"
        },
        "name": {
            "type": "string"
        },
        "daily_food": {
            "type": "number"
        },
        "daily_sleep": {
            "type": "number"
        },
    },
    "required": ["age", "name", "daily_food", "daily_sleep"]
}
```
Проверяем структуру ответа с помощью tiny validator:
```
pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(respBody, schema)).to.be.true;
});
console.log(tv4.error);
```

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
### 5.2 Проверка структуры json в ответе

Составляем JSON Schema для нашего объекта:
```
var schema = {
    "type": "object",
    "properties": {
        "age": {
            "type": "string"
        },
        "salary": {
            "type": "integer"
        },
        "name": {
            "type": "string"
        },
        "family": {
            "type": "object",
            "properties": {
                "u_salary_1_5_year": {
                    "type": "integer"
                },
                "children": {
                    "type": "array",
                    "items": [
                        { "type": "array",
                        items: [
                            { "type": "string" },
                            { "type": "integer" }
                        ] },
                        { "type": "array",
                        items: [
                            { "type": "string" },
                            { "type": "integer" }
                        ] }
                    ]
                }               
            },
            "required": ["children", "u_salary_1_5_year"]
        }
    },
    "required": ["age", "name", "salary", "family"]
}
```
Проверяем структуру ответа с помощью tiny validator:
```
pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(respBody, schema)).to.be.true;
});
console.log(tv4.error);
```
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

## 6. Endpoint /currency

Отправить запрос
`POST http://54.157.99.22:80/currency`

Body: form-data

## 7. Endpoint /curr_byn

Отправить запрос
`POST http://54.157.99.22:80/curr_byn`

Body: form-data

### 7.1 Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### 7.2 Проверка структуры json в ответе

Составляем JSON Schema для нашего объекта:
```
var schema = {
    "type": "object",
    "properties": {
        "Cur_Abbreviation": {
            "type": "string"
        },
        "Cur_ID": {
            "type": "integer"
        },
        "Cur_Name": {
            "type": "string"
        },
        "Cur_OfficialRate": {
            "type": "float"
        },
        "Cur_Scale": {
            "type": "integer"
        },
        "Date": {
            "type": "string"
        }
    },
    "required": ["Cur_Abbreviation", "Cur_ID", "Cur_Name", "Cur_OfficialRate", "Cur_Scale", "Date"]
}
```
Проверяем структуру ответа с помощью tiny validator:
```
pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(respBody, schema)).to.be.true;
});
console.log(tv4.error);
```


