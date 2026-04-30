# CASO CAMPUS
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/LOGO.png" width="350" title="hover text">
</p>

**SHOOTOUT** es una empresa dedicada al arriendo de canchas de futbol, ubicada en el sector sur oriente de la Región Metropolitana.
El gran logro de esta empresa es el haber sido uno de los primeros centros deportivos en consolidar un sistema de programación de partidos de futbol en sus canchas para todo publico y con diferentes categorías de equipos.
La empresa además de su efectividad en la programación del uso de sus canchas, se caracteriza por entregar información de los partidos que se realizan en sus locaciones a los equipos que las utilizan. Dicha información, muchas veces es relevante para estos equipos, ya que a menudo son empresas las que logran formarlos dentro de la organización, para formar campeonatos internos que se juegan en las canchas de **SHOOTOUT**.
Por los motivos descritos, se le ha contactado para reestructurar y automatizar la extracción de información, con el objetivo de brindar a sus clientes un servicio mas completo y detallado de los partidos que se juegan en el recinto.

1.- La base del negocio es el tener la información de la programación y de los equipos que han realizado reservado las canchas, para disponer de esta información, se le solicita extraer programación de los partidos, en el formato y orden descrito a continuación. Debe indicar el estado de la programación como NO JUGADO (‘NJ’), en caso contrario la información del estado debe aparecer como JUGADO, además los datos deben estar ordenados por fecha ascendente y  hora ascendente.


--RESPUESTA
SELECT 
EQUIPO_1||' VS '|| EQUIPO_2 AS "PARTIDO",
SUBSTR(equipo_1,1,3) || ' VS ' || SUBSTR(equipo_2,1,3) AS "ABREVIATURA",
FECHA AS "FECHA_PARTIDO",
TO_CHAR(HORA,'HH24:MI') AS "INICIO",
CASE ESTADO
WHEN 'NJ' THEN 'NO JUGADO'
WHEN 'J' THEN 'JUGADO' END AS "ESTADO"
FROM PROGRAMACION
ORDER BY "FECHA_PARTIDO" ASC, "INICIO" ASC;
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/RESPUESTA1.png" title="hover text">
</p>


2.- Así como se muestra la programación, también es relevante detallar la información de los partidos, sin embargo, en este segmento se consideran solamente los partidos jugados entre el 25 y 29 de agosto, con sus respectivos resultados, además se debe detallar el equipo que juega de local, el que juega de visita, la cancha y la fecha del encuentro. Como dato adicional debe mencionar al ganador del encuentro (LOCAL, VISITA) o mencionar EMPATE en caso que el marcador esté igualado, los datos deben ser ordenados por fecha del partido descendente y  equipo local ascendente.


--RESPUESTA
SELECT 
TO_CHAR(FECHA,'DD/MM/YY') AS "FECHA",
CANCHA,
EQUIPO_LOCAL AS "LOCAL",
EQUIPO_VISITA AS "VISITA",
GOLES_LOCAL||'-'||GOLES_VISITA AS "MARCADOR FINAL",
CASE
WHEN GOLES_LOCAL>GOLES_VISITA THEN 'LOCAL'
WHEN GOLES_LOCAL<GOLES_VISITA THEN 'VISITA'
ELSE
'EMPATE'
END AS "GANADOR"
FROM PARTIDO
WHERE FECHA BETWEEN '25/08/18' AND '29/08/18'
ORDER BY FECHA DESC, EQUIPO_LOCAL ASC;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/RESPUESTA2.png" title="hover text">
</p>


3.- Entre las garantías que otorga SHOOTOUT, está la de mantener a la audiencia de los partidos 100% informada; para este efecto, se registran todos los eventos que ocurren en los partidos. Estos eventos, pueden ser vistos por la audiencia en tiempo real (real time)  y para que esto suceda, usted debe proveer al departamento de comunicaciones y RRSS, la información de los eventos ocurridos en los partidos, con el siguiente orden y formato: evento (minuto ‘, tipo evento, , equipo del jugador,  jugador con camiseta entre paréntesis ej: (11), partido (abreviado con las 3 primeras letras de cada equipo + V/S, ej: BRA v/s CHI ) y la fecha del partido. Solo debe listar eventos hasta  15 días de ocurridos, ordenados por fecha y minuto del evento descendente.


--RESPUESTA
SELECT
MINUTO || '''GOL PARA' || EQUIPO_JUGADOR || ': ' || SUBSTR(NOMBRE_JUGADOR,1,1)
|| ',' || APELLIDO_JUGADOR || '(' || CAMISETA || ')' AS "EVENTO",
SUBSTR(EQUIPO_LOCAL,1,3) || ' VS ' || SUBSTR(EQUIPO_VISITA,1,3) AS "PARTIDO",
TO_CHAR(FECHA,'DD/MM/YY') AS "FECHA"
FROM EVENTO
--SIMULAREMOS QUE NOS ENCONTRAMOS EN UNA FECHA CERCANA PARA CUMPLIR LA CONDICION DE LOS 15 DIAS Y OBTENER DATOS
--PERO LA SENTENCIA REAL ES WHERE FECHA BETWEEN CURRENT_DATE-15 AND CURRENT_DATE;
WHERE FECHA BETWEEN TO_DATE('05/09/18')-15 AND TO_DATE('05/09/18');
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/RESPUESTA3.png" title="hover text">
</p>


4.- En el ámbito administrativo, se requieren de ciertos indicadores para tomar decisiones y guiar el negocio a buenos puertos. Una de estas decisiones contempla el sistema de remuneraciones de los empleados de SHOOTOUT, los que comisionan un porcentaje de cada partido que les toca observar, esto debido a que son ellos los que registran la información de los eventos y estadísticas propias de los partidos. Para este efecto, se desea saber username del usuario que observa y toma registro de los partidos, la cantidad de partidos observados, minutos totales observados, y la comisión a percibir que corresponde al 10,2% de la suma de los valores finales cobrados de cada partido observado. Tenga en cuenta que la tarifa se aplica por cada 60 minutos de partido, o el proporcional en la ocupación de la cancha. Se debe extraer la información desde el primer al último día de agosto del año actual y se debe ordenar por comisión final ascendente.


--RESPUESTA
SELECT
USU.USERNAME AS "USUARIO",
COUNT(PAR.ID_USER) AS "PARTIDOS_OBSERVADOS",
SUM(PRO.MINUTOS_JUGADOS) AS "MINUTOS_OBSERVADOS",
TRIM(TO_CHAR(SUM(PRO.MINUTOS_JUGADOS*(TAR.VALOR/60))*0.102,'$999G999')) AS "COMISION FINAL"
FROM PARTIDO PAR
INNER JOIN USUARIO USU ON USU.ID_USER=PAR.ID_USER
INNER JOIN PROGRAMACION PRO ON PRO.ID_PROGRAMACION=PAR.ID_PROGRAMACION
INNER JOIN TARIFA TAR ON TAR.ID_TARIFA=PAR.ID_TARIFA
--AL IGUAL QUE EN LA RESPUESTA ANTERIOR SIMULAREMOS LA FECHA
--RESPUESTA REAL -> WHERE PRO.MINUTOS_JUGADOS IS NOT NULL AND EXTRACT(MONTH FROM PRO.FECHA)=8 AND EXTRACT(YEAR FROM PRO.FECHA)=EXTRACT(YEAR FROM CURRENT_DATE)
WHERE PRO.MINUTOS_JUGADOS IS NOT NULL AND EXTRACT(MONTH FROM PRO.FECHA)=8 AND EXTRACT(YEAR FROM PRO.FECHA)=2018
GROUP BY USU.USERNAME;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/RESPUESTA4.png" title="hover text">
</p>


5.- Para incentivar la participación de la comunidad y de los equipos que se han registrado en SHOOTOUT, la empresa ha decidido realizar un descuento a los equipos afiliados. El descuento consiste en que SHOOTOUT abonará el 15% del valor pagado en la última visita, al próximo valor final del arriendo siguiente, al equipo que convoque como local del encuentro. Para aplicar el descuento, se le solicita a usted extraer un informe que contenga los partidos con fecha y hora, equipos locales (L) y visita(V), valor pagado y abono que se realizará al equipo que pagará el arriendo. La oferta aplica para equipos locales que hayan rentado una cancha entre los días 25 al 29 de agosto del año 2018, y que hayan completado el partido, en caso que el partido no se haya completado, los valores se deben mostrar con un “$0”. Los partidos deben estar ordenados por fecha de forma descendente.


--RESPUESTA
SELECT
TO_CHAR(PAR.INICIO,'DD/MM/YYYY HH24:MI') AS "FECHA",
TO_CHAR(PAR.INICIO,'HH24:MI') AS "HORA",
PAR.EQUIPO_LOCAL AS "LOCAL",
PAR.EQUIPO_VISITA AS "VISITA",
TO_CHAR(PRO.VALOR_PAGADO,'$999G999') AS "VALOR_PAGADO",
CASE
WHEN PAR.FIN IS NULL THEN '$0'
ELSE TRIM(TO_CHAR(PRO.VALOR_PAGADO*0.15,'$999G999'))
END AS "ABONO PRROMOCION"
FROM PARTIDO PAR
JOIN PROGRAMACION PRO ON PRO.ID_PROGRAMACION=PAR.ID_PROGRAMACION
WHERE PAR.INICIO BETWEEN '25/08/18' AND '29/08/18'
ORDER BY PAR.INICIO ASC;
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/RESPUESTA5.png" title="hover text">
</p>


6.- Por lo general, los equipos acostumbran a pagar un abono para reservar la cancha y al final del encuentro cancelan el saldo o remanente del valor total de la tarifa aplicada. Se ha detectado que en algunos casos, no se han informado los minutos jugados a las programaciones, por ende no se pueden obtener los saldos pendientes. Para mantener esto en monitoreo, se le solicita un informe que muestre la información de cada equipo que tiene un saldo pendiente. El informe debe contener nombre de los equipos, minutos jugados, tarifa aplicada, total a pagar, monto abonado y saldo a pagar. En caso de que los minutos jugados no se hayan encontrado, se deben mostrar como “NO INFORMADOS” y el saldo a pagar debe mostrar “SALDO PENDIENTE” ya que sin los minutos es imposible sacar el saldo pendiente. Debe ordenar por saldo a pagar descendente.


--RESPUESTA
SELECT
PAR.EQUIPO_LOCAL AS "EQUIPO_LOCAL",
PAR.EQUIPO_VISITA AS "EQUIPO_VISITA",
CASE
WHEN PRO.MINUTOS_JUGADOS IS NULL THEN 'NO INFORMADOS'
ELSE TO_CHAR(PRO.MINUTOS_JUGADOS)
END AS "MINUTOS JUGADOS",
TRIM(TO_CHAR(TAR.VALOR,'$999G999')) AS "TARIFA_APLICADA",
CASE
WHEN PRO.MINUTOS_JUGADOS IS NULL THEN 'SALDO PENDIENTE'
ELSE TRIM(TO_CHAR((PRO.MINUTOS_JUGADOS/60)*TAR.VALOR,'$999G999'))
END AS "TOTAL_PARCIAL",
TRIM(TO_CHAR(PRO.VALOR_PAGADO,'$999G999')) AS "ABONADO",
CASE
WHEN PRO.MINUTOS_JUGADOS IS NULL THEN 'SALDO PENDIENTE'
ELSE TRIM(TO_CHAR(((PRO.MINUTOS_JUGADOS/60)*TAR.VALOR)-PRO.VALOR_PAGADO,'$999G999'))
END AS "SALDO_A_PAGAR"
FROM PARTIDO PAR
INNER JOIN PROGRAMACION PRO ON PRO.ID_PROGRAMACION = PAR.ID_PROGRAMACION
INNER JOIN TARIFA TAR ON TAR.ID_TARIFA = PAR.ID_TARIFA
ORDER BY "SALDO_A_PAGAR" DESC;
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_CAMPUS_SQL/IMAGENES/RESPUESTA6.png" title="hover text">
</p>
