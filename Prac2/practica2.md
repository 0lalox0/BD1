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

### 9 TORNEOS (#torneo, nombre_torneo, año, #equipo, nombre_equipo, estadio_equipo, puesto,
#reglamentacion, descripcion, #auspiciante)

● De cada torneo, se conoce su identificador (#torneo, único en el sistema) y un nombre.
Un mismo torneo tiene diferentes ediciones, cada edición se realiza en un año
determinado y el mismo torneo no puede repetirse el mismo año. En un año pueden
realizarse varios torneos.
● Cada edición de un torneo tiene diferentes auspiciantes, identificados por #auspiciante
(único en el sistema).
● En cada edición de un torneo participan varios equipos. De cada equipo se conoce su
nombre, su estadio y su #equipo, que no se repite para diferentes equipos.
● Cada equipo finaliza una edición de un torneo en un puesto. Dos o más equipos no
pueden finalizar en un mismo puesto.
● Además, se conoce un conjunto de reglamentaciones, identificadas por
#reglamentación, aplicables a estos torneos.


Se analiza


DF1  #Torneo -> nombre_torneo
DF2  #Equipo -> nombre_equipo,estadio_equipo
DF3  #Torneo,Ano,Equipo -> Puesto
DF4  Puesto,Ano,#Torneo -> Equipo

CC{**#Torneo,#Equipo,Ano,#Auspiciante,#Reglamentacion,Desc_R**}
CC{**#Torneo,Ano,Puesto,#Auspiciante,#Reglamentacion,Desc_R**}

se elije la clave candidate {**#Torneo,#Equipo,Ano,#Auspiciante,#Reglamentacion,Desc_R**}

El esquema Torneo no se encuentra en BCNF puesto que existe la DF2, la cual es valida en el esquema y su determinante {#Equipo} no es superclave del esquema por lo tanto particionamos el esquema en 2 F1 Y F2 siguiendo DF2: #Equipo -> nombre_equipo,estadio_equipo

F1(#Equipo,nombre_equipo,estadio_equipo)
F2(#torneo, nombre_torneo, año, #equipo, puesto,#reglamentacion, descripcion, #auspiciante)

Si realizamos F1 V F2 -> {#Equipo}. #Esquipo es clave del esquema F1 por lo que no perdemos info
No se pierden df ya que en F1 valen DF2 y en F2 valen DF1,DF3,DF4

F1 esta en BCNF ya que solo vale la df2 y el determinante de la df2 es superclave del esquema

F2 no esta en BCNF puesto que tiene al menos el determinante de df1 no es superclave del esquema.
puesto particionamos el esquema en 2 F3 Y F4 siguiendo la DF1: #Torneo -> nombre_torneo

F3(#Torneo, nombre_torneo)
F4(#torneo, año, #equipo, puesto,#reglamentacion, descripcion, #auspiciante)

Si realizamos F3 V F4 -> {#Torneo}. #Torneo es clave del esquema F3 por lo que no perdemos info
No se pierden DF ya que en F3 valen DF1 y en F4 valen DF3,DF4

F3 esta en BCNF ya que solo vale la df1 y el determinante de la df1 es superclave del esquema

F4 No esta en BCNF puesto que tiene al menos el determinante de df3 no es superclave del esquema.
puesto que particionamos el esquema en 2 F5 Y F6 siguiendo la DF3: #Torneo,Ano,Equipo -> Puesto

F5(#Torneo,Ano,Equipo,Puesto)
F6(#torneo, año, #equipo,#reglamentacion, descripcion, #auspiciante)


F5 esta en bcnf ya que en ella solo valen DF3 Y DF4 cuyo determinantes: {#Torneo,Ano,Equipo},{#Torneo,Ano,Puesto} son superclaves de F5
si realizamos F5 V F6 -> {#Torneo,Ano,Equipo}. #Torneo,Ano,Equipo es clave del esquema F5 no se pierde informacion

F6 esta BNCF puesto que no tiene DF no triviales de las cuales su determinantes no son superclave del esquema, en este caso no tiene df no triviales

Resultado: 

F1(#Equipo,nombre_equipo,estadio_equipo)
F3(#Torneo, nombre_torneo)
F5(#Torneo,Ano,Equipo,Puesto)
F6(#torneo, año, #equipo,#reglamentacion, descripcion, #auspiciante)

Clave: {**#Torneo,#Equipo,Ano,#Auspiciante,#Reglamentacion,Desc_R**}


DM :

    DM1: ANO,#TORNEO ->> #AUSPICIANTES
    DM2: ANO,#TORNEO ->> #Equipo
    DM3: {} ->> #reglamentacion
    DM4: {} ->> desc


F6 esta en BCNF pero no esta en 4FN debido a que existe la DM1 la cual no es trivial por lo que particionamos usando DM1: ANO,#TORNEO ->> #AUSPICIANTES

F7(ANO,#TORNEO, #AUSPICIANTES) 
F8(#torneo, año, #equipo,#reglamentacion, descripcion)

F7 esta en 4FN ya que no valen dependecias multivaluadas que no sean triviales

F8 esta en BCNF pero no esta en 4FN debido a que existe la DM2 la cual no es trivial, por lo que particionamos usando DM2:DM2: ANO,#TORNEO ->> #Equipo

F9(ANO,#TORNEO, #Equipo)
F10(#torneo, año,#reglamentacion, descripcion)

F9 esta en 4FN ya que no valen dependecias multivaludas que no sean triviales

F10 esta en BCNF pero no esta en 4FN debido a que existe la DM3 la cual no es trivial, por lo que particionam,os usando DM3:{} ->> #reglamentacion




esquemas en 4fn:

F1(#Equipo,nombre_equipo,estadio_equipo)
F3(#Torneo, nombre_torneo)
F5(#Torneo,Ano,Equipo,Puesto)
F7(ANO,#TORNEO, #AUSPICIANTES) 
F9(ANO,#TORNEO, #Equipo)
F11(#reglamentacion)
F13(descripcion)
F14(#torneo, año)


esquemas sin proyeciones

F14 es una proyecion de F5,F7,F9 ya puede deducirse a travez de los atributos de ese esquema se elimina del mismo

resultado: 

F1(#Equipo,nombre_equipo,estadio_equipo)
F3(#Torneo, nombre_torneo)
F5(#Torneo,Ano,Equipo,Puesto)
F7(ANO,#TORNEO, #AUSPICIANTES) 
F9(ANO,#TORNEO, #Equipo)
F11(#reglamentacion)
F13(descripcion)

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


Dependencias Funcionales

Df1 #evento -> fecha_evento, motivo_evento, #salon, #grupo
Df2 #salon -> nombre_salon 
Df3 #grupo -> nombre_grupo, nro_ingresantes_grupo, #organizador
Df4 #organizador -> nombre_organizador, telefono_organizador, años_exp_organizador
Df5 fecha_evento, #organizador -> #grupo !!!
Df6 #persona_staff -> nombre_persona_staff, telefono_persona_staff, rol_persona_staff

CC:{#evento,#persona_staff}

ORGANIZACION_EVENTOS no esta en BCNF ya que existe por lo menos DF6 que es valida en el esquema y su determinantes {#persona_staff} no es superclave del esquema.
Por lo tanto particionamos por DF6
O1{*#persona_staff*,nombre_persona_staff, telefono_persona_staff, rol_persona_staff }
O2{*#evento*, fecha_evento, motivo_evento, #salon,
nombre_salon, #grupo, nombre_grupo, nro_integrantes_grupo, #organizador,
nombre_organizador, telefono_organizador, años_exp_organizador, *#persona_staff*}

O1 esta en BCNF ya que solo es valida la DF6 y su determinante {#persona_staff} es superclave de O1.
No se pierde informacion ya que al realizar la validacion simple vemos que O1 v O2 = {#persona_staff} es clave de O1
No se pierden DFs ya que en O1 son validas DF6, y en O2 son Validas Df1,DF2,DF3,DF4,DF5

O2 no esta en BCNf ya que al menos vale la DF4 la cual el determinante {#organizador} no es superclave del esquema O2
por lo que particionamos O2 por DF4
O3{*#organizador*,nombre_organizador, telefono_organizador, años_exp_organizador}
O4{*#evento*, fecha_evento, motivo_evento, #salon,nombre_salon,
 #grupo, nombre_grupo, nro_integrantes_grupo, #organizador, *#persona_staff*}

O3 esta en BCNF ya que solo vale la DF4 de la cual su determinante {#organizador} es superclave del esquema O3
Si realziamos la validacion simple: O3 v O4 = {#organizador} el cual es calve de O3 por lo que no perdemos informacion
No se pierden DFs porque en O3 vale DF4 y en O4 valen Df1,2,3,5

O4 no esta en BCNF porque existe al menos la DF2 la cual es valida en el esquema y su determinante {#salon} no es superclave del esuqema por lo que particionamos por DF2 a O4

O5{*#salon*, nombre_salon}
O6{*#evento*, fecha_evento, motivo_evento, #salon,#grupo,
 nombre_grupo, nro_integrantes_grupo, #organizador, *#persona_staff*}

O5 esta en BCNF ya que en el solo vale la DF2 la cual su determinante es superclave de esquema O5
No se pierde informacion ya que al hacer la validacion simple: O5 v O6 = {#salon} el cual es clave de O5
NO se pierden DFs ya que en O5 vale df2 y en O6 df1, df3,df5

O6 No esta en BCNF ya que al menos vale la DF3 y su determinante {#grupo} no es superclave del esquema O6
por lo tanto particiomanos por DF3

O7{*#grupo*,nombre_grupo, nro_ingresantes_grupo, #organizador}
O8{*#evento*, fecha_evento, motivo_evento, #salon,#grupo, *#persona_staff*}



Df1 #evento -> fecha_evento, motivo_evento, #salon, #grupo
Df2 #salon -> nombre_salon 
Df3 #grupo -> nombre_grupo, nro_ingresantes_grupo, #organizador
Df4 #organizador -> nombre_organizador, telefono_organizador, años_exp_organizador
Df5 fecha_evento, #organizador -> #grupo !!!
Df6 #persona_staff -> nombre_persona_staff, telefono_persona_staff, rol_persona_staff



O7{*#grupo*,nombre_grupo, nro_ingresantes_grupo, #organizador}
O8{*#evento*, fecha_evento, motivo_evento, #salon,#grupo, *#persona_staff*}


O7 esta en BCNF porque solo vale la DF3 en el y #grupo es superclave de O7
No se pierde informacion ya que por validacion simple: O7 v O8 = #grupo que es calve de O7
En O7 vale DF3 y en O8 valen Df1
Que paso con Df5, se pierde por lo tanto se lleva els esquema a 3FN, volvemos un paso atras antes de la particion de O6
y partimos O6 por DF5 para 3fn
O6{*#evento*, fecha_evento, motivo_evento, #salon,#grupo,
 nombre_grupo, nro_integrantes_grupo, #organizador, *#persona_staff*}

O7{*fecha_evento, #organizador*, #grupo}
Solo vale Df5 y el determinante es superclave
particiono por df3
O8{*#grupo*, nombre_grupo, nro_ingresantes_grupo, #organizador}
Solo vale Df3 y el determinante es superclave
particiono por df1
O9{*#evento*,fecha_evento, motivo_evento, #salon, #grupo}
Solo vale Df1 y el determinante es superclave
O10{*#evento*,*persona_staff*}
Esquemas en 3fn yaque no tiene DF no triviales 




select #grupo from O7, O8 where #organidor = #1 and #fecha_evento = 12/03/2023 
12/03/2023,#1 -> #grupo= 2
● De los organizadores se conoce su nombre, teléfono y los años de experiencia que lleva
en su trabajo. También tiene asociado un número que lo identifica.
● Cada organizador tiene contrato con muchos grupos, sin embargo este solo organiza
cada una de sus fechas disponibles con un único grupo, que será el que toque la noche
del evento.
● Cada evento contrata a una serie de personas que serán el staff del mismo. De cada
uno de estos se conoce un identificador, único en el sistema, el nombre, el teléfono y el
rol que ocupa.
O1{*#persona_staff*,nombre_persona_staff, telefono_persona_staff, rol_persona_staff }
O3{*#organizador*,nombre_organizador, telefono_organizador, años_exp_organizador}
O5{*#salon*, nombre_salon}
O7{*#grupo*,nombre_grupo, nro_ingresantes_grupo, #organizador}
O8{*#evento*, fecha_evento, motivo_evento, #salon,#grupo, *#persona_staff*}
Mientras Res cambia
Para i= 1 _a_ cant_de_ particiones_realizadasRes = 
Res ∪((Res ∩ Ri)+ ∩ Ri)

Res = fecha_evento, #organizador
#### O1
Res ∪((Res ∩ O1)+ ∩ O1)

Res = fecha_evento, #organizador
#### O3
Res ∪((Res ∩ O3)+ ∩ O3)
Res U((#organizador)+ v O3)
Res U O3
Res = O3 + fecha_evento
##O5
Res ∪((Res ∩ O5)+ ∩ O5)
Res ∪((0)+ ∩ O5)
Res = O3 + fecha_evento
#### O7
Res ∪((Res ∩ O7)+ ∩ O7)
Res ∪((#organizador)+ ∩ O7)
Res U (#organizador)
Res = O3 + fecha_evento
#### O8
Res U ((Res v O8 )+ v O8)
Res U fecha_evento



### 13. PAGOS (#empleado, dni, nombre, fecha_ingreso, #sucursal, ciudad, telefono,
#departamento, #pago, monto_pago, fecha_pago, #honorario, descripcion_h, monto_h)
● La inmobiliaria dispone de varias sucursales, identificada por #sucursal, de las cuales se
conoce la ciudad donde está ubicada y un teléfono de contacto
● De cada empleado, que trabaja únicamente en una sucursal, se conoce su número
interno (no se repite para diferentes empleados de la inmobiliaria), dni, nombre y fecha
de ingreso.
● Los #identifican un departamento en alquiler que administra la inmobiliaria y no puede
repetirse en las diferentes sucursales. La inmobiliaria asigna a cada departamento
varios empleados para que los administren.
● Los #pagos son secuenciales para cada departamento que posee la inmobiliaria (no
pueden repetirse para el mismo departamento) y se almacena el monto y la fecha de
dicho pago. No se registra la sucursal donde se realizó el pago.
● La inmobiliaria registra todos los honorarios que percibe, de estos se conoce su
#honorario (único en el sistema), el monto y una descripción.

Dependencias Funcionales
DF1 #sucursal -> ciudad, telefono
Df2 #empleado -> #sucursal, dni, nombre, fecha_ingreso
Df3 dni -> #sucursal, #empleado , nombre, fecha_ingreso
Df4 #departamento -> #sucursal No Va
Df5 #departamento,#pago -> monto_pago, fecha_pago
Df6 #honorario -> monto_h , descripcion_h

CC1{#empleado, #departamento, #pago,#honorario}
CC2{dni,#departamento, #pago, #honorario}


Pagos no esta en BCNF ya que existe por lo menos la DF1, la cual es valida en el esquema y su determinantes #sucursal no es superclave del esquema. Por lo tanto particionamos Pagos por df1

P1(*#sucursal*,ciudad,telefono)
P2(#empleado, dni, nombre, fecha_ingreso, #sucursal,#departamento,
 #pago, monto_pago, fecha_pago, #honorario, descripcion_h, monto_h)

P1 esta en BCNF ya que solo es valida la df1 en el y su determinante {#sucursal} es superclave de P1
No se pierde informacion ya que por validaccion simple vemos que P1 v P2 = #sucursal la cual es clave en P1
No se pierden DFs ya que en P1 valen df1 y en P2 valen el resto

P2 no esta en BCNF ya que por lo menos vale Df2 en ella y su determinante{#empleado} no es superclave de p2
por lo tanto particionamos P2 por la Df2

P3(*#empleado*,#sucursal, dni, nombre, fecha_ingreso)
P4(#empleado,#departamento,#pago, monto_pago,
 fecha_pago, #honorario, descripcion_h, monto_h)

 P3 esta en BCNF ya que solo valen df2 y df3 en ella y dni y #cliente son sus determinatnes y superclave
 No se pierde informacion ya que p3 v p4 = #empleado q es clave de p3
 No dfs se pirden ya que en p3 valen df2 y 3 y en p4 df5 y df6
 P4 no esta en BCNF porque existe por lo menos df5 cuyo determinante {departamento,¨Pago} no es superclave del esquema
 por lo tanto particionamos P4 por la df5
 P5(**#departamento,#pago**, monto_pago, fecha_pago)
P6(#empleado,#departamento,#pago, #honorario, descripcion_h, monto_h)
 
 P5 esta en BCV

 P6 
 P7(*#honorario*,monto_h , descripcion_h)
 P8(#empleado,#departamento,#pago,#honorario)

 x
Clave Primaria:{#empleado, #departamento, #pago,#honorario}
 Dms
dm1#departamento -> #empleado
dm2#departamento ->  #pago
dm3{} > #honorario

P9(*#honorario*)
P9 esta en 4FN porque no tiene dependencias multivaluadas no triviales

p10(#empleado,#departamento,#pago)
P10 no esta en 4Fn porque en ella vale la DM2 la cual no es trivial

P11(#departamento,#pago)
P11 esta en 4FN porque no tiene dependencias multivaluadas no triviales

P12(#departamento,#empleado)
P12 esta en 4FN porque no tiene dependencias multivaluadas no triviales

Tablas finales en 4FN que no son proyecciones
(P11 es proyeccion de p5
P9 es proyeccion de P7
)
P1(*#sucursal*,ciudad,telefono)
P3(*#empleado*,#sucursal, dni, nombre, fecha_ingreso)
P5(**#departamento,#pago**, monto_pago, fecha_pago)
P7(*#honorario*,monto_h , descripcion_h)
P12(*#departamento,#empleado*)


### 10. DISPOSITIVOS (marca_id, descripMarca, modelo_id, descripModelo, equipo_tipo_id,
descripEquipoTipo, nombreEmpresa, cuit, direcciónEmpresa, usuario_id, apyn,
direcciónUsuario, cuil, plan_id, descripPlan, importe, equipo_id, imei, fec_alta, fec_baja,
observaciones, línea_id, fec_alta_linea, fec_baja_linea)
Donde:
● Para cada equipo interesa conocer su tipo, modelo, imei, fecha en que se dio de alta,
fecha en que se da de baja y las observaciones que sean necesarias.
● De cada marca se conoce su descripción
● De cada modelo se conoce su descripción y a qué marca pertenece.
● Para cada plan, se registra qué empresa lo brinda, descripción e importe del mismo.
● Para cada tipo de equipo se conoce la descripción
● Para cada empresa se registra el nombre, cuit y dirección
● De cada usuario se registra su nombre y apellido, número de documento, dirección y
CUIL
● Para cada línea se necesita registrar qué plan posee, la fecha de alta de la línea, la
fecha de baja, el equipo que la posee y el usuario de la misma.

Df1 marca_id -> descipMarca X
Df2 modelo_id -> descripModelo X
Df3 plan_id -> descripPlan, importe, cuit X
df4 equipo_tipo_id -> descipEquipoTipo X
Df5 cuit -> nombreEmpresa, direccionEmpresa
Df6 cuil -> apyn, direccionUsuario, usuario_id
Df7 usuario_id-> apyn, direccionUsuario, cuil 
Df8 linea_id -> fec_alta_linea, fec_baja_linea, plan_id, usuario_id, equipo_id
Df9 linea_id -> fec_alta_linea, fec_baja_linea, plan_id, cuil, equipo_id
df10 equipo_id -> imei, fec_alta,fec_baja equipo_tipo_id, modelo_id, marca_id  X

CC{*linea_id,observaciones*}
Dispositivos no este en BCNF yaque existe la Df1 la cual es valida en este esquema y su determinante marca_id no es superclave del esquema, por lo tanto particionamos F1 por df1
F1(*marca_id*, descipMarca)
F2(*marca_id*,, modelo_id, descripModelo, equipo_tipo_id,
descripEquipoTipo, nombreEmpresa, cuit, direcciónEmpresa, usuario_id, apyn,
direcciónUsuario, cuil, plan_id, descripPlan, importe, equipo_id, imei, fec_alta, fec_baja,
observaciones, línea_id, fec_alta_linea, fec_baja_linea)
F1 estaen BCNF yaque solo es valida en el la df1 y marca_id el determinate de la misma es superclave de F1
No se pierde INformacion yaque por validacion simple da F1 v F2 = marca_id clave de F1
No se pierde Dfs ya que en F2 valen el resto de Dfs y en f1 vale Df1

F3(*modelo_id*, descripModelo)
F5(*equipo_tipo_id*, descipEquipoTipo)
F7(*cuit*, nombreEmpresa, direccionEmpresa)
F9(*plan_id*,descripPlan, importe, cuit)
F11(*equipo_id*,imei, fec_alta,fec_baja equipo_tipo_id, modelo_id, marca_id )
f12(usuario_id, apyn,direcciónUsuario, 
cuil, plan_id, equipo_id,observaciones, 
línea_id, fec_alta_linea, fec_baja_linea)

F13(*usuario_id*,apyn, direccionUsuario, cuil)
F14(usuario_id, plan_id, equipo_id,observaciones, 
línea_id, fec_alta_linea, fec_baja_linea)
F13 esta en BCNF ya que en solo son validas Df6 y 7  y sus determinantes {usuario_id} y {cuil} son superclaves del esquema
no se pierde info yaque f13 v f14 = usuario_id la cual es clave en f13
no se pierden dfs ya que en f13 valen df6 y 7 y en f14 valen df8
y no queda valida df9 pero no se pierde ya que de manera indirecta podemos conseguir los determinados con su determinante atraves de df8 linea_id -> usuario_id y df7 usuario_id -> cuil y de manera directa en f14 conseguimos el resto de los atributos determinados por df9

F15(*linea_id*,fec_alta_linea, fec_baja_linea, plan_id, usuario_id, equipo_id)
F16(*linea_id,observaciones*)
no hay dms no triviales

Esquemas en 4FN
F1(*marca_id*, descipMarca)
F3(*modelo_id*, descripModelo)
F5(*equipo_tipo_id*, descipEquipoTipo)
F7(*cuit*, nombreEmpresa, direccionEmpresa)
F9(*plan_id*,descripPlan, importe, cuit)
F11(*equipo_id*,imei, fec_alta,fec_baja equipo_tipo_id, modelo_id, marca_id )
F13(*usuario_id*,apyn, direccionUsuario, cuil)
F15(*linea_id*,fec_alta_linea, fec_baja_linea, plan_id, usuario_id, equipo_id)
F16(*linea_id,observaciones*)