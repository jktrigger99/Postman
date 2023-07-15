## Homework #2

### http://162.55.220.72:5005/first

### 1. Отправить запрос

`GET http://162.55.220.72:5005/first`

### 2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### 3. Проверить, что в body приходит правильный string
```
pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("This is the first responce from server!ss");
});
```

### http://162.55.220.72:5005/user_info_3

### 1. Отправить запрос

`POST http://162.55.220.72:5005/user_info_3`

Body - form-data

### 2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### 3. Спарсить response body в json

`var respBody = pm.response.json()`

### 4. Проверить, что name в ответе равно name в запросе (name вбить руками)
```
var req_name = reqBody.name
pm.test("Check name is " + req_name, function () {   
    pm.expect(respBody.name).to.eql("Evgeny");
});
```
### 5. Проверить, что age в ответе равно age в запросе (age вбить руками)
```
var req_age = reqBody.age
pm.test("Check age is " + req_age, function () {   
    pm.expect(respBody.age).to.eql("39");
});
```
### 6. Проверить, что salary в ответе равно salary в запросе (salary вбить руками)
```
var req_salary = reqBody.salary
pm.test("Check salary is " + req_salary, function () {   
    pm.expect(respBody.salary).to.eql(1000);
});
```
### 7. Спарсить request

`var reqBody = request.data`

### 8. Проверить, что name в ответе равно name в запросе (name забрать из request)
```
pm.test("Check name is " + req_name, function () {   
    pm.expect(respBody.name).to.eql(req_name);
});
```
### 9. Проверить, что age в ответе равно age в запросе (age забрать из request)
```
pm.test("Check age is " + req_age, function () {   
    pm.expect(respBody.age).to.eql(req_age);
});
```
### 10. Проверить, что salary в ответе равно salary в запросе (salary забрать из request)
```
pm.test("Check salary is " + req_salary, function () {   
    pm.expect(respBody.salary).to.eql(+req_salary);
});
```
### 11. Вывести в консоль параметр family из response

`console.log(respBody.family)`

### 12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```
pm.test("Check salary after 1,5 years is " + (+req_salary * 4), function () {   
    pm.expect(respBody.family.u_salary_1_5_year).to.eql(+req_salary * 4);
});
```

### http://162.55.220.72:5005/object_info_3

### 1. Отправить запрос

`GET http://162.55.220.72:5005/object_info_3?name=Evgeny&age=39&salary=1000`

### 2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### 3. Спарсить response body в json

`var respBody = pm.response.json()`

### 4. Спарсить request

`var req_url = pm.request.url.query.toObject()`

### 5. Проверить, что name в ответе равно name в запросе (name забрать из request)
```
var req_name = req_url.name
pm.test("Check name is " + req_name, function () {   
    pm.expect(respBody.name).to.eql(req_name);
});
```
### 6. Проверить, что age в ответе равно age в запросе (age забрать из request)
```
var req_age = req_url.age
pm.test("Check age is " + req_age, function () {   
    pm.expect(respBody.age).to.eql(req_age);
});
```
### 7. Проверить, что salary в ответе равно salary в запросе (salary забрать из request)
```
pm.test("Check salary is " + req_salary, function () {   
    pm.expect(respBody.salary).to.eql(+req_salary);
});
```
### 8. Вывести в консоль параметр family из response

`console.log(respBody.family)`

### 9. Проверить, что у параметра dog есть параметры name
```
var respDog = respBody.family.pets.dog
pm.test("Check that dog has a name", function () {   
    pm.expect(respDog).to.have.property("name")
});
```
### 10. Проверить, что у параметра dog есть параметры age
```
pm.test("Check that dog has age", function () {   
    pm.expect(respDog).to.have.property("age")
});
```
### 11. Проверить, что параметр name имеет значение Luky
```
pm.test("Check dog's name is Luky", function () {   
    pm.expect(respDog.name).to.eql("Luky");
});
```
### 12. Проверить, что параметр age имеет значение 4
```
pm.test("Check dog's age is 4", function () {   
    pm.expect(respDog.age).to.eql(4);
});
```

### http://162.55.220.72:5005/object_info_4

### 1. Отправить запрос.

`GET http://162.55.220.72:5005/object_info_4?name=John&age=30&salary=5000`

### 2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### 3. Спарсить response body в json

`var respBody = pm.response.json()`

### 4. Спарсить request

`var req_url = pm.request.url.query.toObject()`

### 5. Проверить, что name в ответе равно name в запросе (name забрать из request)
```
var req_name = req_url.name
pm.test("Check name is " + req_name, function () {   
    pm.expect(respBody.name).to.eql(req_name);
});
```
### 6. Проверить, что age в ответе равно age из request (age забрать из request)
```
pm.test("Check age is " + req_age, function () {   
    pm.expect(respBody.age).to.eql(+req_age);
});
```
### 7. Вывести в консоль параметр salary из request

`console.log(req_salary)`

### 8. Вывести в консоль параметр salary из response

`console.log(respBody.salary)`

### 9. Вывести в консоль 0-й элемент параметра salary из response

`console.log(respBody.salary[0])`

### 10. Вывести в консоль 1-й элемент параметра salary из response

`console.log(respBody.salary[1])`

### 11. Вывести в консоль 2-й элемент параметра salary из response

`console.log(respBody.salary[2])`

### 12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request)
```
pm.test("Check salary is " + req_salary, function () {   
    pm.expect(respBody.salary[0]).to.eql(+req_salary);
});
```
### 13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request)
```
pm.test("Check salary is " + req_salary*2, function () {   
    pm.expect(+respBody.salary[1]).to.eql(req_salary*2);
});
```
### 14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request)
```
pm.test("Check salary is " + req_salary*3, function () {   
    pm.expect(+respBody.salary[2]).to.eql(req_salary*3);
});
```
### 15. Создать в окружении переменную name
### 16. Создать в окружении переменную age
### 17. Создать в окружении переменную salary
### 18. Передать в окружение переменную name

`pm.environment.set("name", respBody.name)`

### 19. Передать в окружение переменную age

`pm.environment.set("age", respBody.age)`

### 20. Передать в окружение переменную salary

`pm.environment.set("salary", respBody.salary[0])`

### 21. Написать цикл, который выведет в консоль по порядку элементы списка из параметра salary.
```
for (var i = 0; i < respBody.salary.length; i++) {
    console.log(respBody.salary[i])
}
```

### http://162.55.220.72:5005/user_info_2
### 1. Вставить параметр salary из окружения в request
### 2. Вставить параметр age из окружения в age
### 3. Вставить параметр name из окружения в name
### 4. Отправить запрос.

`POST http://162.55.220.72:5005/user_info_2`

### 5. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
### 6. Спарсить response body в json

`var respBody = pm.response.json()`

### 7. Спарсить request

`var reqBody = request.data`

### 8. Проверить, что json response имеет параметр start_qa_salary
```
pm.test("Check that response has the start_qa_salary parameter", function () {   
    pm.expect(respBody).to.have.property("start_qa_salary")
});
```
### 9. Проверить, что json response имеет параметр qa_salary_after_6_months
```
pm.test("Check that response has the qa_salary_after_6_months parameter", function () {   
    pm.expect(respBody).to.have.property("qa_salary_after_6_months")
});
```
### 10. Проверить, что json response имеет параметр qa_salary_after_12_months
```
pm.test("Check that response has the qa_salary_after_12_months parameter", function () {   
    pm.expect(respBody).to.have.property("qa_salary_after_12_months")
});
```
### 11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
```
pm.test("Check that response has the qa_salary_after_1.5_year parameter", function () {   
    pm.expect(respBody).to.have.property("qa_salary_after_1.5_year")
});
```
### 12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
```
pm.test("Check that response has the qa_salary_after_3.5_years parameter", function () {   
    pm.expect(respBody).to.have.property("qa_salary_after_3.5_years")
});
```
### 13. Проверить, что json response имеет параметр person
```
pm.test("Check that response has the person parameter", function () {   
    pm.expect(respBody).to.have.property("person")
});
```
### 14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request)
```
pm.test("Check that request and response salaries are equal", function () {   
    pm.expect(respBody.start_qa_salary).to.eql(+req_salary);
});
```
### 15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request)
```
pm.test("Check that request salary*2 = qa_salary_after_6_months", function () {   
    pm.expect(respBody.qa_salary_after_6_months).to.eql(+req_salary*2);
});
```
### 16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request)
```
pm.test("Check that request salary*2.7 = qa_salary_after_12_months", function () {   
    pm.expect(respBody.qa_salary_after_12_months).to.eql(+req_salary*2.7);
});
```
### 17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request)
```
pm.test("Check that request salary*3.3 = qa_salary_after_1.5_year", function () {   
    pm.expect(respBody["qa_salary_after_1.5_year"]).to.eql(+req_salary*3.3);
});
```
### 18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request)
```
pm.test("Check that request salary*3.8 = qa_salary_after_3.5_years", function () {   
    pm.expect(respBody["qa_salary_after_3.5_years"]).to.eql(+req_salary*3.8);
});
```
### 19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request)
```
pm.test("Check that request salary = u_name[1]", function () {   
    pm.expect(respBody.person.u_name[1]).to.eql(+req_salary)
});
```
### 20. Проверить, что что параметр u_age равен age из request (age забрать из request)
```
pm.test("Check that request age = u_age", function () {   
    pm.expect(respBody.person.u_age).to.eql(+req_age)
});
```
### 21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request)
```
pm.test("Check that request salary*4.2 = u_salary_5_years", function () {   
    pm.expect(respBody.person.u_salary_5_years).to.eql(+req_salary*4.2);
});
```
### 22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person
```
for (i in respBody.person) {
    if (typeof respBody.person[i] == "object") {
        for (j in respBody.person[i]) {
           console.log(`${i}: ${respBody.person[i][j]}`) 
        }
    }
    else {
        console.log(`${i}: ${respBody.person[i]}`) 
        }
}
```

