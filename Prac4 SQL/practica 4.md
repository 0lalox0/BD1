### 2) 
Hallar aquellos pacientes que para todas sus consultas médicas siempre hayan
dejado su número de teléfono primario (nunca el teléfono secundario).
```sql
select distinct p.patient_id from patient p
 INNER JOIN appointment a on p.patient_id = a.patient_id
 where contact_phone = primary_phone and p.patient_id not in(
select distinct p2.patient_id from patient p2
INNER JOIN appointment a2 on p2.patient_id = a2.patient_id 
where a2.contact_phone = p2.secondary_phone);
````


### 3)
Crear una vista llamada ‘doctors_per_patients’ que muestre los id de los pacientes y
los id de doctores de la ciudad donde vive el cliente

Create VIEW doctors_per_patients  AS ( select patient_id , doctor_id from patient, doctor 
where patient_city = doctor_city)

### 4)
Hallar los pacientes (únicamente es necesario su id) que se atendieron con todos los
doctores de la ciudad en la que viven
a. Realice la consulta sin utilizar la vista creada anteriormente
b. Realice la consulta utilizando la vista creada anteriormente
Restricción: resolver este ejercicio sin usar la cláusula NOT EXIST


a)
SELECT patient_id from patient where patient_id not in (
SELECT DISTINCT patient_id FROM (
select patient_id , doctor_id from patient, doctor 
where patient_city = doctor_city 
except
select patient_id , doctor_id from medical_review) as temp);

b)
SELECT patient_id from patient where patient_id not in (
SELECT DISTINCT patient_id FROM (
select * from doctors_per_patients
except
select patient_id , doctor_id from medical_review) as temp);

### 5) 
Agregar la siguiente tabla:
APPOINTMENTS_PER_PATIENT
idApP: int(11) PK AI
id_patient: int(11)
count_appointments: int(11)
last_update: datetime
user: varchar(16)

CREATE TABLE APPOINTMENTS_PER_PATIENT (
idApP integer auto_increment primary key,
id_patient integer(11),
count_appointments integer(11),
last_update datetime,
user varchar(16)
);


### 6)
Crear un Stored Procedure que realice los siguientes pasos dentro de una
transacción:
a. Realizar una consulta que para cada pacient (identificado por id_patient),
calcule la cantidad de appointments que tiene registradas. Registrar la fecha
en la que se realiza esta carga y además del usuario con el se realiza.
b. Guardar el resultado de la consulta en un cursor.
c. Iterar el cursor e insertar los valores correspondientes en la tabla
APPOINTMENTS PER PATIENT.

DELIMITER //
CREATE PROCEDURE contarAppointments (IN loaded_by_user VARCHAR(100))
BEGIN
	DECLARE cant integer;
    DECLARE id integer;
    declare fin integer default 0;
	DECLARE contados cursor for
	SELECT patient_id, count(patient_id) 
    FROM appointment
    GROUP BY patient_id;
    DECLARE CONTINUE handler for not found set fin = 1;
    START TRANSACTION;
	OPEN contados ;
		loop_cursor : loop
        fetch next from contados into id, cant;
        IF fin = 1 then
			leave loop_cursor;
		end if;
        insert into appointments_per_patient (id_patient, count_appointments, last_update, user)
        values (id,cant,now(),loaded_by_user);
    END LOOP;
    CLOSE contados;
    COMMIT;
END //
DELIMITER ; 

### 7)
Crear un Trigger de modo que al insertar un dato en la tabla Appointment, se
actualice la cantidad de appointments del paciente, la fecha de actualización y el
usuario responsable de la misma (actualiza la tabla APPOINTMENTS PER
PATIENT).

DELIMITER //

CREATE TRIGGER actCount
AFTER INSERT ON appointment
FOR EACH ROW
BEGIN
    DECLARE cant INT;

    -- Calcular el nuevo total de citas para el paciente
    SELECT COUNT(*) INTO cant
    FROM appointment
    WHERE patient_id = NEW.patient_id;
    
    -- Verificar si ya existe un registro en appointments_per_patient para el paciente
    IF EXISTS (SELECT 1 FROM appointments_per_patient WHERE patient_id = NEW.patient_id) THEN
        -- Actualizar el conteo y la fecha en caso de que el registro ya exista
        UPDATE appointments_per_patient
        SET count = cant,
            updated_at = NOW(),
            updated_by = NEW.loaded_by_user  -- Suponiendo que loaded_by_user viene en la tabla appointment
        WHERE patient_id = NEW.patient_id;
    ELSE
        -- Insertar un nuevo registro si no existe uno para el paciente
        INSERT INTO appointments_per_patient (patient_id, count, updated_at, updated_by)
        VALUES (NEW.patient_id, cant, NOW(), NEW.loaded_by_user);
    END IF;
END //

DELIMITER ;