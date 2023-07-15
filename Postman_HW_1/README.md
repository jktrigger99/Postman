## Homework #1

Protocol: http

IP: 162.55.220.72

Port: 5005

### EP_1
Method: GET

EndPoint: /get_method

request url params: 
- name: str
- age: int

Request:

`GET http://162.55.220.72:5005/get_method?name=Evgeny&age=38`

Response:

`Status: 200 OK`

```
[
    "Evgeny",
    "38"
]
```

### EP_2

Method: POST

EndPoint: /user_info_3

request body (form-data): 
- name: str
- age: int
- salary: int

Request:

`POST http://162.55.220.72:5005/user_info_3`

Response:

`Status: 200 OK`

```
{
    "age": "38",
    "family": {
        "children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        "u_salary_1_5_year": 4000
    },
    "name": "Evgeny",
    "salary": 1000
}
```

### EP_3

Method: GET

EndPoint: /object_info_1

request url params: 
- name: str
- age: int
- weight: int

Request:

`GET http://162.55.220.72:5005/object_info_1?name=Evgeny&age=38&weight=66`

Response:

`Status: 200 OK`

```
{
    "age": 38,
    "daily_food": 0.792,
    "daily_sleep": 165.0,
    "name": "Evgeny"
}
```

### EP_4

Method: GET

EndPoint: /object_info_2

request url params: 
- name: str
- age: int
- salary: int

Request:

`GET http://162.55.220.72:5005/object_info_2?name=Evgeny&age=38&salary=1000`

Response:

`Status: 200 OK`

```
{
    "person": {
        "u_age": 38,
        "u_name": [
            "Evgeny",
            1000,
            38
        ],
        "u_salary_5_years": 4200.0
    },
    "qa_salary_after_1.5_year": 3300.0,
    "qa_salary_after_12_months": 2700.0,
    "qa_salary_after_3.5_years": 3800.0,
    "qa_salary_after_6_months": 2000,
    "start_qa_salary": 1000
}
```

### EP_5

Method: GET

EndPoint: /object_info_3

request url params: 
- name: str
- age: int
- salary: int

Request:

`GET http://162.55.220.72:5005/object_info_3?name=Evgeny&age=38&salary=1000`

Response:

`Status: 200 OK`

```
{
    "age": "38",
    "family": {
        "children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        "pets": {
            "cat": {
                "age": 3,
                "name": "Sunny"
            },
            "dog": {
                "age": 4,
                "name": "Luky"
            }
        },
        "u_salary_1_5_year": 4000
    },
    "name": "Evgeny",
    "salary": 1000
}
```

### EP_6

Method: GET

EndPoint: /object_info_4

request url params: 
- name: str
- age: int
- salary: int

Request:

`GET http://162.55.220.72:5005/object_info_4?name=Evgeny&age=38&salary=1000`

Response:

`Status: 200 OK`

```
{
    "age": 38,
    "name": "Evgeny",
    "salary": [
        1000,
        "2000",
        "3000"
    ]
}
```


### EP_7

Method: POST

EndPoint: /user_info_2

request body (form-data): 
- name: str
- age: int
- salary: int

Request:

`POST http://162.55.220.72:5005/user_info_2`

Response:

`Status: 200 OK`

```
{
    "person": {
        "u_age": 38,
        "u_name": [
            "Evgeny",
            1000,
            38
        ],
        "u_salary_5_years": 4200.0
    },
    "qa_salary_after_1.5_year": 3300.0,
    "qa_salary_after_12_months": 2700.0,
    "qa_salary_after_3.5_years": 3800.0,
    "qa_salary_after_6_months": 2000,
    "start_qa_salary": 1000
}
```
