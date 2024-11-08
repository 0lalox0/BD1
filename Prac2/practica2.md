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
