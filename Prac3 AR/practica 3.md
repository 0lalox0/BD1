Π σ |X|
### 4) Chekeado
PASAJERO (#pasajero, nombre, dni, puntaje) 
PASAJERO_RESERVA (#pasajero, #reserva) 
RESERVA (#reserva, #vuelo, fecha_reserva, monto, #asiento) 
VUELO (#vuelo, aeropuerto_salida, aeropuerto_destino, fecha_vuelo) 
C) Obtener el/los pasajeros que solo hayan reservado vuelos cuyo aeropuerto de 
salida sea el aeropuerto “Ministro Pistarini”. Listar el nombre y dni de los 
pasajeros. 
VUELOS_PISTARINI <-  Π #vuelo (σ aeropuerto_salida=“Ministro Pistarini” VUELO ) 
RESERVA_PISTARINI <-  Π #pasajero (VUELOS_PISTARINI |X| RESERVA) 
PASAJEROS_PISTARINI <-  Π nombre,dni (RESERVA_PISTARINI |X| PASAJERO) 

Falso: Reserva no tiene # pasajero

D) Obtener el/los id/s de los pasajeros que hayan realizado reservas por un 
monto superior a $99000 
 
RESERVAS_MAS_99000 <- Π #pasajero (σ monto < 99000 RESERVA)

Reserva no tiene # pasajero

### 6) Choferes 
 
DUEÑO ( id_dueño, nombre, teléfono, dirección, dni ) 
CHOFER ( id_chofer, nombre, teléfono, dirección, fecha_licencia_desde, 
fecha_licencia_hasta, dni ) 
AUTO ( patente, id_dueño, id_chofer, marca, modelo, año ) 
     VIAJE ( patente, hora_desde, hora_hasta, origen, destino, tarifa, metraje ) 
  
a) Listar el dni, nombre y teléfono de todos los dueños que NO son choferes 
b) Listar la patente y el id_chofer de todos los autos a cuyos choferes les caduca la licencia el 
01/01/2024

Supongo que dni es unico
a) dueñosychofer <- P(id_dueño,nombre,telefono,direcicon,dni)(Dueño |X| Chofer)
    Res <- Dueño - dueñosychofer
b)
    Res <- AUTO |X|P(id_chofer)S(fecha_licencias_hasta = "01/01/2024")(Chofer)

### 7) Estudiantes y carreras 
 
ESTUDIANTE ( #legajo, nombreCompleto, nacionalidad, añoDeIngreso, 
códigoDeCarrera ) 
CARRERA ( códigoDeCarrera, nombre ) 
INSCRIPCIONAMATERIA ( #legajo, códigoDeMateria ) 
MATERIA ( códigoDeMateria, nombre ) 
  
a) Obtener el nombre de los estudiantes que ingresaron en 2019. 
 
b) Obtener el nombre de los estudiantes con nacionalidad “Argentina” que NO estén en la 
carrera con código “LI07” 
 
c) Obtener el legajo de los estudiantes que se hayan anotado en TODAS las materias. 
 
a) p(nombreCompleto)s(añoDeIngreso = 2019)ESTUDIANTE

b)Argentinos <- s(nacionalidad = "Argentina")ESTUDIANTE
  cursanLI07 <- (Argentinos |X| s(codigoDeMateria = "LI07")INSCRIPCIONAMATERIA)
  Argentinos - cursanLI07

c) INSCRIPCIONAMATERIA % p(codigoDeMateria)MATERIA 


### 8) Cursos 
 
LUGAR_TRABAJO ( #empleado, #departamento ) 
CURSO_EXIGIDO ( #departamento, #curso ) 
CURSO_REALIZADO ( #empleado, #curso ) 

a) ¿Quiénes son los empleados que han hecho todos los cursos, independientemente de qué 
departamento los exija? 
 
b) ¿Quiénes son los empleados que ya han realizado todos los cursos exigidos por sus 
departamentos?

a) CURSO_REALIZADO % p(#curso)CURSO_EXIGIDO

b) cursosARealizar <- p(#empleado, #curso)(LUGAR_TRABAJO |X| CURSO_EXIGIDO)
   cursosqueFaltan <- cursosARealizar - (CURSO_REALIZADO)
   CURSO_REALIZADO - cursosqueFaltan


### 9) Fabricantes de Muebles  Repaso
 
TIPOMUEBLE ( id_tipomueble, descripción ) 
FABRICANTE ( id_fabricante,nombrefabricante, cuit ) 
TIPOMADERA ( id_tipomadera, nombremadera ) 
AMBIENTE ( id_ambiente, descripcionambiente ) 
MUEBLE ( id_mueble, id_tipomueble, id_fabricante, id_tipomadera, precio, dimensiones, 
descripcion ) 
MUEBLEAMBIENTE ( id_mueble, id_ambiente ) 
 
 
 .  Obtener los nombres de los fabricantes que fabrican muebles en todos los tipos de 
madera. 
a.  Obtener los nombres de los fabricantes que sólo fabrican muebles en Pino. 
b.  Obtener los nombres de los fabricantes que fabrican muebles para todos los ambientes. 
c.  Obtener los nombres de los fabricantes que sólo fabrican muebles para oficina. 
d.  Obtener los nombres de los fabricantes que sólo fabrican muebles para baño y cocina. 
e.  Obtener los nombres de los fabricantes que producen muebles de cedro y roble. 
f.  Obtener los nombres de los fabricantes que producen muebles de melamina o MDF 
 