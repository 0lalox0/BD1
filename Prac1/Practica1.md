 6) Pozos Petroleros 
Una compañía petrolera debe monitorear parámetros ambientales sobre los pozos en los que opera. Cada pozo se encuentra en una posición geográfica (latitud y longitud), tiene un nombre y una fecha de puesta en producción. Sobre cada pozo se realizan monitoreos periódicos con la intención de registrar distintas variables de interés y de los cuales se debe guardar la fecha del 
monitoreo y el método aplicado en el mismo. En cada monitoreo se miden diferentes parámetros(suelen repetirse entre mediciones), de los cuales se conoce un nombre y un valor de referencia.  Además, en cada monitoreo, para cada parámetro específico, se obtiene un resultado, del cual se guarda el valor obtenido y el instrumento que se utilizó. Los instrumentos que se utilizan en los monitoreos pueden ser analógicos o digitales. De los analógicos se tiene la última fecha de calibración, y de los digitales se conoce la marca y modelo. De todos los instrumentos se conoce el número de 


![alt text](<punto6.drawio (1).png>)


#### Paso a Modelo Relacional

Pozo(**Latitud,Longitud**,nombre,fecha)
Realizan(**#Monitoreo**,Latitud,Longitud)
Monitoreo(**#Monitoreo**,fecha, Metodo)
Mide(**#Monitoreo,Nombre**)
Parametro(**Nombre**,Valor_Referencia)
Obtiene(**#Monitoreo,Nombre**,#Resultado)
Resultado(**#Resultado**,Valor)
Se Utilizo(**#Resultado**,Numero_Serie)
Instrumento(**Numero_Serie**,tipo,calibracion,marca,modelo)
o
Se UtilizoDigi(**#Resultado**,Numero_Serie)
Se UtilizoAna(**#Resultado**,Numero_Serie)
Analogico(**Numero_Serie**,Calibracion)
Digital(**Numero_serie**,marca,modelo)
