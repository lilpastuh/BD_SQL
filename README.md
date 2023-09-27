# BD_SQL

# Грищук Александр Олегович 153505
# Тема - Полицейский участок

# Functional requirements:

    •	User authorization
    •	User management (CRUD)
    •	The role system (roles: FELON, POLICEMAN, ADMIN)
    •	Logging user actions
    •	Police rank&specializations CRUD (ADMIN)
    •	Schedule CRUD (ADMIN)
    •	Services CRUD (ADMIN)
    •	Appointments CRUD (FELON, POLICEMAN)
    •	Criminal article CRUD (POLICEMAN)
    •	Prescriptions CRUD (POLICEMAN)

# Use-case

1. Non-authorized user
   
    See policemen list
    See policemen's services list
    See reception time
    Authorize
   
2. Authorized user
   
  2.1. Felon
  
      See policemen list
      See policemen's services list
      See reception time
      Make an appointment
      
  2.2. Policemen
  
      See their appointments
      Felon criminal articles CRUD
      Prescriptions CRUD
      
  2.3. Admin
  
CRUD with all entities

# Таблицы

user

    id BIGSERIAL PRIMARY KEY NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(50) NOT NULL,
    FOREIGN KEY role_id REFERENCES role(id) NOT NULL
    
user_activity

    id BIGSERIAL PRIMARY KEY NOT NULL,
    FOREIGN KEY user_id REFERENCES user(id) NOT NULL,
    activity_type VARCHAR(255) NOT NULL,
    date_of_activity DATE NOT NULL,
    time_of_activity TIME NOT NULL
    
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
    
policeman_rank

    id SERIAL PRIMARY KEY NOT NULL,
    rank_name VARCHAR(25) UNIQUE NOT NULL

reception_time_slot

    id BIGSERIAL PRIMARY KEY NOT NULL,
    date_reception DATE NOT NULL,
    time_reception TIME NOT NULL,
    FOREIGN KEY doctor_id REFERENCES policeman(id) NOT NULL,
    is_free BOOLEAN NOT NULL DEFAULT FALSE
    
service

    id SERIAL PRIMARY KEY NOT NULL,
    service_name VARCHAR(50) NOT NULL,
    price DECIMAL(12,2) NOT NULL,
    FOREIGN KEY policeman_id REFERENCES policeman(id) NOT NULL
    
appointment

    id BIGSERIAL PRIMARY KEY NOT NULL,
    FOREIGN KEY time_slot_id REFERENCES reception_time_slot(id) NOT NULL,
    FOREIGN KEY felon_id REFERENCES felon(id) NOT NULL,
    FOREIGN KEY lawyer_id REFERENCES lawyer(id)
    
appointment_service (MTM)

    id BIGSERIAL PRIMARY KEY NOT NULL,
    FOREIGN KEY appointment_id REFERENCES appointment(id) NOT NULL,
    FOREIGN KEY service_id REFERENCES service(id) NOT NULL
    
criminal_article

    id SERIAL PRIMARY KEY NOT NULL,
    article_name VARCHAR(50) NOT NULL,
    article_number VARCHAR(10) NOT NULL
    
lawyer

    id BIGSERIAL PRIMARY KEY NOT NULL,
    note TEXT NOT NULL,
    FOREIGN KEY appointment_id REFERENCES appointment(id) NOT NULL
    
felon_article (MTM)

    id BIGSERIAL PRIMARY KEY NOT NULL,
    FOREIGN KEY felon_id REFERENCES felon(id) NOT NULL,
    FOREIGN KEY article_id REFERENCES criminal_article(id) NOT NULL,
    date_of_article DATE NOT NULL,
    note TEXT
 

