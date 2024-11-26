1)
    2. Tiene mas de una clave candidata
2)
    3 cc(a,f)
### 3)
Indicar la opción correcta
Dada la relación:
ALUMNO (DNI, nyAp, nroLegajo, promedio, #libroUsadoEnCarrera)
En la que se cumple las siguientes dependencias funcionales:
DF1) DNI → nyAp, nroLegajo, promedio
DF2) nroLegajo → nyAp, DNI, promedio
¿Cuál de las siguientes afirmaciones es correcta?
a) La relación ALUMNO tiene dos claves candidatas y tendrá dos claves primarias.
b) La relación ALUMNO tiene dos claves candidatas y tendrá una clave primaria. V
c) No puedo identificar una clave.
d) Ninguna de las anteriores.

### 4)

Dependencias funcionales
Dado el siguiente esquema:
TIENDA (#aplicacion, nombre_aplicacion, descripcion, #categoria, #etiqueta,
#desarrollador, nombre_apellido_desarrollador, #actualizacion,
descripcion_cambios)
Donde:
● #aplicacion, #categoria, #etiqueta y #desarrollador son únicos en el sistema.
● Una aplicación tiene un nombre y una descripción, y puede actualizarse muchas
veces
● Para cada actualización de una aplicación se registra un texto con los cambios
realizados. El #actualización es secuencial, cada aplicación define los suyos y
puede repetirse entre distintas aplicaciones.
● Cada aplicación tiene una única categoría y muchas etiquetas. Las etiquetas
pueden ir cambiando con cada actualización de la aplicación (en cada
actualización puede haber un conjunto diferente de etiquetas). La categoría
nunca cambia, es decir que se mantiene igual sin importar las actualizaciones.
● Una aplicación es realizada por varios desarrolladores de los cuales se conoce
su nombre y apellido.
Seleccione las DFs válidas / mínimas: Para las que no se seleccionen, indicar el
motivo.
1) #aplicacion, #actualizacion -> nombre_aplicacion, descripcion X
2) #aplicacion, #actualizacion -> descripcion_cambios V
3) nombre_apellido_desarrollador -> #desarrollador
4) #desarrollador -> nombre_apellido_desarrollador V
5) #aplicación -> #categoria V
Encontró alguna dependencia funcional más, que no se menciona entre las opciones?
NO
o
6) #aplicacion -> nombre_aplicacion, descripcion

### 5)
Dependencias multivaluadas
Dado el siguiente esquema:
CURSOS(#curso, titulo_curso, #nro_modulo, titulo_modulo, contenido_modulo,
nombre_autor, email_autor, contraseña_autor, año_edicion, calificacion,
referencia)
Donde:
● Cada curso (#curso) se va editando todos los años, y en cada año (año_edicion)
puede cambiar sus módulos, no así el título y el autor.
● En cada año que se edita un curso, recibe varias calificaciones anónimas.
● El email de cada autor se usa como login, y no puede repetirse en el sistema.
● Los números de módulo (#nro_modulo) son secuenciales (modulo 1, 2, 3, etc).
Es decir, en cada edición de cada curso se enumeran los módulos de la misma
forma, y se pueden repetir en diferentes ediciones de cursos.
● Cada curso tiene múltiples referencias bibliográficas, que se mantienen a través
de todas sus ediciones.
Dadas las siguientes DF:
● #curso -> titulo_curso, email_autor
● #curso, año_edicion, #nro_modulo -> titulo_modulo, contenido_modulo
● email_autor -> nombre_autor, contraseña_autor
Dada la siguiente CC:
● (#curso, año_edicion, #nro_modulo, calificacion, referencia)
Y el esquema en BCNF
CURSOS_N (#curso, año_edicion, #nro_modulo, calificacion, referencia)
Seleccione las DM que son válidas a la vez en el esquema CURSOS_N:
● #curso ->> año_edicion
● #curso ->> referencia
● #curso,año_edicion ->> calificacion
● referencia ->> #curso
● año_edicion ->> #curso
Existe alguna dependencia multivaluada más que no se menciona entre las opciones?
#curso ->> #nro_modulo ? 
o
#crso, año_edicion ->> #nro_modulo


## Parte 2
Dados los siguientes esquemas, realizar todo el proceso de normalización hasta 4FN.
Indicar los esquemas finales válidos resultantes del proceso y la FN en la que quedan   
### 6.
SUSCRIPCION (#suscripcion, email, nombre_usuario, #plan, nombre_plan,
texto_condiciones, precio, email_adicional, nombre_adicional, #contenido, titulo, sinopsis,
duracion, fecha_adicional)
Donde:
● Cada suscripción es realizada por un único usuario (identificado por el email) y un plan,
pero además hay usuarios adicionales que la utilizan (email_adicional). De cada usuario
adicional que se suma a la suscripción, se guarda la fecha.
● Un plan de suscripción tiene un nombre (que no puede garantizarse que sea único en el
sistema), condiciones, y un precio mensual.
● Cada contenido tiene un título, sinopsis y duración. El #contenido es único en el
sistema, pero del título no puede garantizarse que lo sea.
● De cada suscripción se sabe qué contenidos fueron reproducidos, sin distinción sobre
qué usuario (titular o adicionales) reprodujo cada uno.

DF1 #suscripcion -> email, #plan X
DF2 email -> nombre_usuario X
DF3 #plan -> nombre_plan, texto_condiciones, precio X
DF4 #suscripcion, email_adicional -> fecha_adicional
DF5 #contenido -> titulo, sinopsis, duracion X
DF6 email_adicional -> nombre_adicional X

CC(#suscripcion, email_adiconal, #contenido)

Particiono por DF3 #plan no es superclave del esquema

I1(**#plan**,nombre_plan,texto_condicones,precio)
I2(**#suscripcion**,email,nombre_usuario,#plan,**email_adicional**,nombre_adicional,fecha_adicional,**#contenido**,titulo,sinopsis,duracion)


I1 esta en BCNF ya que plan es superclave del esquema y solo vale DF3 en este

No se pierde información ya que I1 ∩I2 es {#plan}, clave de I1.

Particiono por DF5 , #contenido no es superclave del esquema

I3(**#contenido**, titulo, sinopsis,duracion)
I4(**#suscripcion**,email,nombre_usuario,#plan,**email_adicional**,nombre_adicional,fecha_adicional,**#contenido**)

I3 esta en BCNF ya que #contenido es superclave del esquema ya que solo vale la DF5
No se pierde información ya que I3 ∩I4 es {#contenido}, clave de I3.

Particiono por DF2

I5(**email**,nombre_usuario)
I6(**#suscripcion**,email,#plan,**email_adicional**,nombre_adicional,fecha_adicional,**#contenido**)

I5 esta en BCNF ya que email es superclave del esquema ya que solo vale la DF1
No se pierde información ya que I5 ∩I6 es {email}, clave de I5.

Particiono por DF6

I7(**email_adicional**,nombre_adicional)
I8(**#suscripcion**,email,#plan,**email_adicional**,fecha_adicional,**#contenido**)

I7 esta en BCNF ya que email es superclave del esquema ya que solo vale la DF6
No se pierde información ya que I7 ∩I8 es {email_adiconal}, clave de I5.

Particiono por DF1

I9(**suscripcion**,email,#plan)

I10(**#suscripcion**,**email_adicional**,fecha_adicional,**#contenido**)

I9 esta en BCNF ya que la suscripcion es superclave del esquema ya que solo vale la DF1
No se pierde información ya que I9 ∩ 10 es {#suscripcion}, clave de I9.

Particiono por DF4

I11(**suscripcion**,**email_adiconal**,fecha_adicional)

I12(**#suscripcion**,**email_adicional**,**#contenido**)

I11 esta en BCNF ya que la **suscripcion** y **email_adiconal** es superclave del esquema ya que solo vale la DF4
No se pierde información ya que I11 ∩ 10 es {#suscripcion,email adicional}, clave de I1.
I12 esta en BCNF ya que es superclave del sistema

Final BCNF
I1(**#plan**,nombre_plan,texto_condicones,precio)
I3(**#contenido**, titulo, sinopsis,duracion)
I5(**email**,nombre_usuario)
I7(**email_adicional**,nombre_adicional)
I9(**suscripcion**,email,#plan)
I11(**suscripcion**,**email_adiconal**,fecha_adicional)
I12(**#suscripcion**,**email_adicional**,**#contenido**)
= francopi

Pasar a 4FN

DM1 #suscripcion ->> email_adicionales
DM2 #suscripcion ->> #contenido


Particiono en DM1

I13(#suscripcion, email_adiconal) 4FN
I14(#suscripcion,#contenido)4FN
DM1 y DM2 pasan a ser dependencias multievaluadas triviales, ya que son todos los atributos de esquema
= juanopi
### 7)
7. MEDICION_AMBIENTAL(#medicion, #pozo, valor_medicion, #parametro, fecha_medicion,
cuil_operario, #instrumento, nombre_parametro, valor_ref, descripcion_pozo,
fecha_perforacion, nombre_parametro, apellido_operario, nombre_operario, fecha_nacimiento,
marca_instrumento, modelo_instrumento, dominio_vehiculo, fecha_adquisicion)
Donde:
● Cada medición es realizada por un operario en un pozo, en una fecha determinada. En
ella se miden varios parámetros, y para cada uno se obtiene un valor. Notar que un
mismo parámetro (#parametro) puede ser medido en diferentes mediciones.
Independientemente de las mediciones, todo parámetro tiene un nombre y valor de
referencia, y el #parametro es único en el sistema.
● En cada medición se utilizan varios instrumentos, independientemente de los
parámetros medidos. De cada instrumento se conoce la marca y modelo.
● De cada operario se conoce su cuit, nombre, apellido y fecha de nacimiento.
● La empresa cuenta con vehículos, y de cada uno se conoce la fecha en la que fue
adquirido. El dominio (patente) de cada vehículo es único en el sistema.
● Un pozo tiene una descripción y una fecha de perforación. El identificador #pozo es
único en el sistema
Dependencias Funcionales

DF1 cuil_operario -> nombre_operario, apellido_operario, fecha_nacimineto X
DF2 #medicion -> #pozo, fecha_medicion, cuil_operario
DF3 #parametro -> nombre_parametro, valor_ref
DF4 #instrumento -> marca_instrumento, modelo_instrumento
DF5 #pozo -> descripcion_pozo, fecha_perforacion X
DF6 dominio_vehiculo ->  fecha_adquisicion
DF7 #medicion, #parametro -> valor_medicion
CC(#medicion, #parametro, #instrumento,dominio_vehiculo)

Nos preguntamos: MEDICION_AMBIENTAL cumple con la definición de BCNF?
NO, dado que existe al menos el determinante de la df1 que NO es superclave del 
esquema MEDICION_AMBIENTAL.
Por lo tanto, particionamos por la DF1, creando dos nuevas relaciones:

I1(**cuil_operario**,nombre_operario,apellido_operario,fecha_nacimiento)

I2(**#medicion** #pozo, valor_medicion, **#parametro**, fecha_medicion,
cuil_operario, **#instrumento**, nombre_parametro, valor_ref, descripcion_pozo,
fecha_perforacion,
marca_instrumento, modelo_instrumento, **dominio_vehiculo**, fecha_adquisicion)

I1 esta en BCNF ya que solo vale DF1 y el determinante CuilOperario es superclave del esquema I1
No se pierde información ya que I1 ∩I2 es {cuil_operario}, clave de I1.

I2 no esta en bcnf ya que existe por lo menos DF5 tiene como determinante #pozo y vale en I2 y no es una superclave de este por lo tanto particionamos

I3(**#pozo**, descripcion_pozo, fecha_perforacion)
I4(**#medicion** #pozo, valor_medicion, **#parametro**, fecha_medicion,
cuil_operario, **#instrumento**, nombre_parametro, valor_ref,
 ,marca_instrumento, modelo_instrumento, **dominio_vehiculo**, fecha_adquisicion)

 Same

 Same

 Particiono por DF2 

I5(**#medicion**, #pozo, fecha_medicion,cuil_operario)
I6(**#medicion** , valor_medicion, **#parametro**, **#instrumento**, nombre_parametro, valor_ref,
 marca_instrumento, modelo_instrumento, **dominio_vehiculo**, fecha_adquisicion)

 Same 
 Same

 Particionoi por DF3
 I7(**#parametro**,nombre_parametro, valor_ref)
 I8(**#medicion** , valor_medicion, **#parametro**, **#instrumento**,marca_instrumento, modelo_instrumento, **dominio_vehiculo**, fecha_adquisicion)

 Particionoi por DF4
 I9(**#instrumento**, marca_instrumento,modelo_instrumento)

 I10(**#medicion** , valor_medicion, **#parametro**, **#instrumento**, **dominio_vehiculo**, fecha_adquisicion)

same
same
Particiono por DF6
I11(**dominio_vehiculo**,fecha_adquicicion)
I12(**#medicion** , valor_medicion, **#parametro**, **#instrumento**, **dominio_vehiculo**)

Particiono por DF7

I13(**#medicion**, **#parametro**,valor_medicion)
I14(**#medicion**, **#parametro**, **#instrumento**, **dominio_vehiculo**)

FIN BCNF

4FN
#medicion -> #parametro
#medicion -> #instrumento
[] -> #dominio_vehiculo
I15(**#medicion, #parametro**)
I16(**medicion,#instrumento**)
I17(**#dominio_vehiculo**)

I15 es una proyeccion de I13?
I17 es una proyeccion de I11?

Se elimina I15 y I17
I13 y I11 no tiene Dm

### 8. FESTIVALES (#festival, denominacion_festival, localidad, cuil_musico, nombre_musico,
fecha_nacimiento, #banda, nombre_banda, estilo_musical, #tema, nombre_tema, duracion,
instrumento, cuil_auspiciante, url_plataforma_entradas, #sponsor)
Donde:
● Para cada festival se conoce su denominación y la localidad en la que se realiza. Más
de un festival podría tener la misma denominación.
● De cada banda se conoce su nombre y estilo musical.
● De cada músico se conoce su cuil, nombre y su fecha de nacimiento. Tenga en cuenta
que varios músicos podrían tener el mismo nombre.
● Para cada tema interpretado por una banda en un festival se conoce su nombre y
duración. Además, de cada músico que participó en el tema se sabe con qué
instrumento lo hizo.
● Los #tema pueden repetirse para las distintas bandas.
● Un festival puede tener varios auspiciantes, y se vendieron entradas al mismo a través
de varias plataformas.
● Se tiene además un registro de todas los sponsors que han participado de los distintos
festivales realizados

DF1) #festival -> denominacion_festival, localidad
DF2) #banda -> nombre_banda, estilo_musical
DF3) cuil_musico -> nombre_musico, fecha_nacimiento
DF4) #tema, #banda, #festival -> nombre_tema, duracion
DF5) #tema, #banda, #festival, cuil_musico -> instrumento

CC(#festival,#banda,cuil_musico,#tema,cuil_auspiciante,url_plataforma_entradas, #sponsor)

Festivales no esta en BCNF yaque existe al menos la DF2 la cual su determinante (#banda) no es superclave del esquema
por lo tanto particiono

F1(*#banda*,nombre_banda,estilo_musical)
F2(*#festival*, *enominacion_festival, localidad, *cuil_musico*, nombre_musico,
fecha_nacimiento, *#banda*, *#tema*, nombre_tema, duracion,
instrumento, *cuil_auspiciante*, *url_plataforma_entradas*, *#sponsor*)

F1 esta en BCNF ya que solo es valida DF2 en ella y su determinante #banda es superclave del esquema
No se pierden Informacion ya que F1 ∩ F2 = #banda la cual es clave de F1
No se pierden DF porque en F2 es valida todas las depenencias menos DF2 y en F1 es valida DF2

F2 no esta en BCNF ya que existe al menos DF3 la cual su determinante  cuil_musico no es superclave del esquema
particiono por DF3

F3(*cuil_musico*,nombre_musico, fecha_nacimiento)

F4(*#festival*, denominacion_festival, localidad, *cuil_musico*, *#banda*, *#tema*, nombre_tema, duracion,
instrumento, *cuil_auspiciante*, *url_plataforma_entradas*, *#sponsor*)

No se pierde informacion ya uqe F3 ∩ F4 = cuil_musico que es clave de F3 
NO se pierden DFs ya que en F3 es valida Df3 y en F4 es valida las otras.


F5(*festival*,denominacion_festival, localidad)

F6(*#festival*, , *cuil_musico*, 
fecha_nacimiento, *#banda*, *#tema*, nombre_tema, duracion,
instrumento, *cuil_auspiciante*, *url_plataforma_entradas*, *#sponsor*)

F7(*#tema*, *#banda*, *#festival*, nombre_tema, duracion)
F8(*#festival*, , *cuil_musico*,  *#banda*, *#tema*, instrumento, *cuil_auspiciante*, *url_plataforma_entradas*, *#sponsor*)

F9(*#tema*, *#banda*, *#festival*,*cuil_auspiciante*,instrumento)
F10(*#festival* , *cuil_musico*,  *#banda*, *#tema*, *cuil_auspiciante*, *url_plataforma_entradas*, *#sponsor*)

Particones en BCNF

F1(*#banda*,nombre_banda,estilo_musical)
F3(*cuil_musico*,nombre_musico, fecha_nacimiento)
F5(*festival*,denominacion_festival, localidad)
F7(*#tema*, *#banda*, *#festival*, nombre_tema, duracion)
F9(*#tema*, *#banda*, *#festival*,*cuil_auspiciante*,instrumento)
F10(*#festival*, *cuil_musico*,  *#banda*, *#tema*, *cuil_auspiciante*, *url_plataforma_entradas*, *#sponsor*)

Clave:(*#festival*,*#banda*,*cuil_musico*,*#tema*,*cuil_auspiciante*,*url_plataforma_entradas*, *#sponsor*)

DM
DM1 #festival ->> cuil_auspiciante
DM2 #festival ->> url_plataforma_entradas
DM3 {} ->> #sponsor
DM4 #banda ->> *cuil_musico* '????
DM5 #banda ->> tema ??????


### 11. ORGANIZACION_EVENTOS (#evento, fecha_evento, motivo_evento, #salon,
nombre_salon, #grupo, nombre_grupo, nro_integrantes_grupo, #organizador,
nombre_organizador, telefono_organizador, años_exp_organizador, #persona_staff,
nombre_persona_staff, telefono_persona_staff, rol_persona_staff)
Donde:
● De cada evento se conoce un identificador, que es único, la fecha, el motivo, el salón de
fiestas donde se desarrollará y el grupo que tocará en el mismo.
● De cada salón de fiestas posible se conoce un número identificador, único en el sistema
y su nombre.
● De los grupos se conoce un identificador (único) su nombre y la cantidad de integrantes
que lo conforman. Además, se sabe que cada grupo de los registrados en el sistema
tiene un contrato de exclusividad con un único organizador.
● De los organizadores se conoce su nombre, teléfono y los años de experiencia que lleva
en su trabajo. También tiene asociado un número que lo identifica.
● Cada organizador tiene contrato con muchos grupos, sin embargo este solo organiza
cada una de sus fechas disponibles con un único grupo, que será el que toque la noche
del evento.
● Cada evento contrata a una serie de personas que serán el staff del mismo. De cada
uno de estos se conoce un identificador, único en el sistema, el nombre, el teléfono y el
rol que ocupa.


