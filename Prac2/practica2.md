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