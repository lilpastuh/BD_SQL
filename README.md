# BD_SQL

# Грищук Александр Олегович 153505
# Тема - Полицейский участок

# Функциональные требования:

    • Авторизация пользователя
    • Управление пользователями (регистрация, удаление аккаунта, просмотр)
    • Ролевая система (роли: Преступник, ПОЛИЦЕЙСКИЙ, АДМИН, АДВОКАТ)
    • Регистрация действий пользователя(логирование).
    • просмотр информации о запросах(полицейский, админ)
    • Полицейские CRUD (Админ)
    • Адвокаты CRUD (АДМИН)
    • Рассмотр заявки(АДВОКАТ)

# Вариант использования

1. Неавторизованный пользователь
   
        Посмотреть список адвокатов
        Авторизоваться
   
2. Авторизованный пользователь
   
  2.1. Преступник
  
     Подать запрос на услуги адвоката
     Просмотр истории своих запросов
      

  2.2. Полицейские
  
       Просмотр истории запросов для обвиняемого
  2.3 Адвокат
  
        Просмотр списка адвокатов
        Рассмотр запроса
  2.4. Админ
  
    CRUD Полицейских и Адвокатов
    и все, что полицейский и адвокат

# Таблицы

user

    id BIGSERIAL PRIMARY KEY NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(50) NOT NULL,
    FOREIGN KEY role_id REFERENCES role(id) NOT NULL
    
    
role

    id SERIAL PRIMARY KEY NOT NULL,
    role_name VARCHAR(25) UNIQUE NOT NULL
    
felon

    id BIGSERIAL PRIMARY KEY NOT NULL,
    FOREIGN KEY user_id REFERENCES user(id) UNIQUE NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE NOT NULL,
    sex VARCHAR(20) NOT NULL,
    phone_number CHAR(13) ~ '\+375[0-9]{9}' NOT NULL,
    
policeman

    id SERIAL PRIMARY KEY NOT NULL,
    FOREIGN KEY user_id REFERENCES user(id) UNIQUE NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    FOREIGN KEY specialization_id REFERENCES policeman_specialization(id) NOT NULL,
    
lawyer

    id BIGSERIAL PRIMARY KEY NOT NULL,
    note TEXT NOT NULL,
    FOREIGN KEY appointment_id REFERENCES appointment(id) NOT NULL


logging

    ID SERIAL PRIMARY KEY,
    log_time TIMESTAMP
    message VARCHAR(32) NOT NULL,
    UserId INT NOT NULL,
    FOREIGN KEY (UserId) REFERENCES Users(ID)

Request

    ID SERIAL PRIMARY KEY,
    CreatedDate TIMESTAMP NOT NULL,
    RequestStatus VARCHAR(32) NOT NULL,
    FelonID INT NOT NULL,
    LawyerID INT NOT NULL,
    PolicemanID INT NOT NULL,
    FOREIGN KEY (FelonID) REFERENCES Felon(ID),
    FOREIGN KEY (LawyerID) REFERENCES Lawyers(ID),
    FOREIGN KEY (PolicemanID) REFERENCES Policeman(ID)

 CarTypes 
 
    ID SERIAL PRIMARY KEY,
    Type VARCHAR(64) NOT NULL

Cars 
    ID SERIAL PRIMARY KEY,
    Model VARCHAR(64) NOT NULL,
    Manufacture_Year DATE NOT NULL,
    cartypesid INT NOT NULL,
    FOREIGN KEY (cartypesid) REFERENCES CarTypes(ID)


# Диаграмма 

![image_2023-12-27_16-29-38](https://github.com/lilpastuh/BD_SQL/assets/94675136/e20d87bc-8e4b-471f-b948-d009863e2d5c)



