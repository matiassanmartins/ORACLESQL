# CASO COBRANZA
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/LOGO.jpg" width="350" title="hover text">
</p>

Con el afán de seguir mejorando sus plataformas, PAY NOW le ha contactado debido a su excelente gestión en las primeras etapas de las automatizaciones realizadas a nivel de extracción de información.
En esta instancia, y luego de haber sostenido una reunión con el staff gerencial, comercial y creativo de la empresa, se han decidido algunas tareas que deberá implementar:
•	El desarrollo de dos nuevos informes enfocados a tomar decisiones comerciales.
•	Incorporación de nuevos registros para notificar deudas.

1.- Uno de los nuevos informes que se requiere, corresponde al stock de casos por empresa desde el año 2015, casos que no se han cobrado por el concepto de notificación y los cuales se han re gestionado en el año 2018.
 Esta información es relevante ya que de ella dependen los pagos que se le efectuarán a PAY NOW por concepto de gestión de cobranza y permitirán realizar las nuevas implementaciones en sus sistemas.
Ya que esta información es importante para la toma de decisiones y contiene valores asociados a las ganancias generadas por PAY NOW, solo podrá ser accedida por los departamentos Gerencia y Planificación. Debe considerar que, para efectos de honorarios, PAY NOW cobra el 7% de la deuda de cada cliente, y el empleado se comisiona un 4% del mismo monto.
Se ha indicado que la información requerida debe contener la empresa, la cantidad total de deudas por empresa, el  stock que  corresponde al total de deudas que se han notificadas, el monto a cobrar correspondiente a la comisión por clientes notificados, el costo correspondiente a la comisión del empleado, y la ganancia que corresponde a la diferencia del monto a cobrar menos el costo asociado a la comisión de los empleados.
Para la integridad de la información, se ha decidido obtenerla mediante la vista VW_STOCK_NOTIFICADO que será definida de solo lectura. La vista debe mostrar los datos ordenados alfabéticamente por empresa y por monto a cobrar en forma descendente.


--RESPUESTA
```sql
    CREATE OR REPLACE VIEW VW_STOCK_NOTIFICADO AS
    SELECT 
    EMP.NOMBRE_EMP AS "EMPRESA",
    (SELECT 
    COUNT(*) 
    FROM DEUDA DEU 
    WHERE DEU.RUT_EMP=EMP.RUT_EMP AND DEU.COD_ESD!=4) AS "STOCK",
    (SELECT
    COUNT(*)
    FROM DEUDA DEU
    INNER JOIN NOTIFICACION NOTI ON NOTI.ID_DEA=DEU.ID_DEA
    WHERE DEU.RUT_EMP=EMP.RUT_EMP AND DEU.COD_ESD!=4 AND NOTI.COD_ESN='N') AS "TOTAL_NOTIFICADAS",
    (SELECT
    TO_CHAR(SUM(DEU.MONTO_DEA*0.07),'$999G999G999')
    FROM DEUDA DEU
    INNER JOIN NOTIFICACION NOTI ON NOTI.ID_DEA=DEU.ID_DEA
    WHERE DEU.RUT_EMP=EMP.RUT_EMP AND DEU.COD_ESD!=4 AND NOTI.COD_ESN='N') AS "MONTO_A_COBRAR",
    (SELECT
    TO_CHAR(SUM(DEU.MONTO_DEA*0.04),'$999G999G999')
    FROM DEUDA DEU
    INNER JOIN NOTIFICACION NOTI ON NOTI.ID_DEA=DEU.ID_DEA
    WHERE DEU.RUT_EMP=EMP.RUT_EMP AND DEU.COD_ESD!=4 AND NOTI.COD_ESN='N') AS "COSTO_EMPLEADO",
    (SELECT
    TO_CHAR(SUM(DEU.MONTO_DEA*0.07)-SUM(DEU.MONTO_DEA*0.04),'$999G999G999')
    FROM DEUDA DEU
    INNER JOIN NOTIFICACION NOTI ON NOTI.ID_DEA=DEU.ID_DEA
    WHERE DEU.RUT_EMP=EMP.RUT_EMP AND DEU.COD_ESD!=4 AND NOTI.COD_ESN='N') AS "GANANCIA"
    FROM EMPRESA EMP
    ORDER BY EMP.NOMBRE_EMP ASC, MONTO_A_COBRAR DESC
    WITH READ ONLY;

    SELECT * FROM VW_STOCK_NOTIFICADO;
```
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA1.png" title="hover text">
</p>


2.- Como incentivo a sus empleados, PAY NOW ha decidido otorgar premios o incentivos a los empleados que hayan logrado que los deudores hayan pagado su deuda mediante la gestión de la notificación, para ello se ha dispuesto que los premios serán a partir de 18 clientes gestionados, y consiste en un aumento en base a la comisión recibida por la cantidad de gestiones realizadas. Se deben contemplar los siguientes tramos:

| CLIENTES GESTIONADOS | PREMIO |
| :---: | :---: |
| 18 a 20 | 10% de incremento |
| 21 a 22 | 12% de incremento |
| Sobre 23 | 15% de incremento |

La información requerida debe ser el nombre del usuario, la cantidad de clientes gestionados, la comisión que recibirá este por la cantidad de clientes gestionados (4% de las deudas de los clientes), el monto del premio, sueldo bruto y el sueldo final que recibirá el empleado. Debe considerar que un trabajador gana un sueldo base bruto de $150.000 el cual aumenta por la comisión, además considerar el cálculo:  sueldo bruto (comisión) + el premio, descontando conceptos de salud y previsión social (20%).  Por motivos de confidencialidad, se ha requerido fijar la consulta como una vista nombrada VW_EMP_SUELDO_COMISION, y debe ser asegurada como solo lectura.
Los resultados deben ser ordenados y formateados.


--RESPUESTA

    CREATE OR REPLACE VIEW VW_EMP_SUELDO_COMISION AS
    SELECT
    USU.NOMBRE_USR||' '||USU.APATERNO_USR AS "USUARIO",
    COUNT(*) AS "CLIENTES_NOTIFICADOS",
    TO_CHAR(SUM(DEU.MONTO_DEA*0.04),'$999G999G999') AS "COMISION",
    CASE
    WHEN COUNT(*) BETWEEN 18 AND 20 THEN TO_CHAR((SUM(DEU.MONTO_DEA*0.04))*0.1,'$999G999G999')
    WHEN COUNT(*) BETWEEN 21 AND 22 THEN TO_CHAR((SUM(DEU.MONTO_DEA*0.04))*0.12,'$999G999G999')
    WHEN COUNT(*) >=23 THEN TO_CHAR((SUM(DEU.MONTO_DEA*0.04))*0.15,'$999G999G999')
    ELSE TO_CHAR(0,'$999G999G999')
    END AS "MONTO_PREMIO",
    CASE
    WHEN COUNT(*) BETWEEN 18 AND 20 THEN TO_CHAR(150000+(SUM(DEU.MONTO_DEA*0.04))*1.1,'$999G999G999')
    WHEN COUNT(*) BETWEEN 21 AND 22 THEN TO_CHAR(150000+(SUM(DEU.MONTO_DEA*0.04))*1.12,'$999G999G999')
    WHEN COUNT(*) >=23 THEN TO_CHAR(150000+(SUM(DEU.MONTO_DEA*0.04))*1.15,'$999G999G999')
    ELSE TO_CHAR(150000+(SUM(DEU.MONTO_DEA*0.04)),'$999G999G999')
    END AS "SUELDO_BRUTO",
    CASE
    WHEN COUNT(*) BETWEEN 18 AND 20 THEN TO_CHAR((150000+(SUM(DEU.MONTO_DEA*0.04))*1.1)*0.8,'$999G999G999')
    WHEN COUNT(*) BETWEEN 21 AND 22 THEN TO_CHAR((150000+(SUM(DEU.MONTO_DEA*0.04))*1.12)*0.8,'$999G999G999')
    WHEN COUNT(*) >=23 THEN TO_CHAR((150000+(SUM(DEU.MONTO_DEA*0.04))*1.15)*0.8,'$999G999G999')
    ELSE TO_CHAR((150000+(SUM(DEU.MONTO_DEA*0.04)))*0.8,'$999G999G999')
    END AS "SUELDO_LIQUIDO"
    FROM USUARIO USU
    INNER JOIN NOTIFICACION NOTI ON NOTI.ID_USR=USU.ID_USR
    INNER JOIN DEUDA DEU ON DEU.ID_DEA=NOTI.ID_DEA
    WHERE NOTI.COD_ESN='N'
    GROUP BY USU.NOMBRE_USR,USU.APATERNO_USR
    ORDER BY CLIENTES_NOTIFICADOS DESC, USUARIO ASC
    WITH READ ONLY;

    SELECT * FROM VW_EMP_SUELDO_COMISION;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA2.png" title="hover text">
</p>


3.- Como parte de la nueva área relacionada con recuperación y recaudación, se ha determinado extraer información relativa a los clientes que tienen más morosidades acumuladas en un rango de 6 meses. Es decir, debe informar a todos los clientes que tengan deudas no cerradas en un periodo de 6 meses a partir de la fecha de la consulta.
La información que se desea visualizar corresponde a el rut del cliente, el nombre, la cantidad de deudas no cerradas que posee, dirección, el teléfono, la suma del monto de sus deudas, el pago mínimo que debe realizar cual corresponde al valor máximo de sus deudas más el 5%, y un pago de repactación cual corresponde al 5% de la deuda total.
Por disposición de la compañía, se ha establecido que la información se llame a través de la vista VW_CLIENTES_RECAUDACION a la que tendrán acceso ciertos usuarios de PAY NOW.
La información se debe ordenar por cantidad de deudas descendente, monto de la deuda descendente, y cliente alfabéticamente. 


--RESPUESTA

    CREATE OR REPLACE VIEW VW_CLIENTES_RECAUDACION AS
    SELECT
    TRIM(TO_CHAR(CLI.RUT_CLE,'99G999G999','NLS_NUMERIC_CHARACTERS = '',.''')||'-'||CLI.DV_CLE) AS "RUT",
    CLI.NOMBRE_CLE||' '||CLI.APATERNO_CLE AS "NOMBRE_CLIENTE",
    COUNT(*) AS "DEUDAS",
    CASE
    WHEN DCL.CALLE_DCL IS NOT NULL THEN DCL.CALLE_DCL
    ELSE '** NO REGISTRA **'
    END AS "DIRECCION",
    CASE
    WHEN DCL.TELEFONO_DCL IS NOT NULL THEN DCL.TELEFONO_DCL
    ELSE '** NO REGISTRA **'
    END AS "TELEFONO",
    TO_CHAR(SUM(DEU.MONTO_DEA),'$999G999G999') AS "MONTO_DEUDA",
    TO_CHAR(MAX(DEU.MONTO_DEA)*1.05,'$999G999G999') AS "PAGO_MINIMO",
    TO_CHAR(SUM(DEU.MONTO_DEA)*0.05,'$999G999G999') AS "PAGO_REPACTACION"
    FROM CLIENTE CLI
    INNER JOIN DEUDA DEU ON DEU.RUT_CLE=CLI.RUT_CLE
    FULL OUTER JOIN DIRECCION_CLIENTE DCL ON DCL.RUT_CLE=CLI.RUT_CLE
    WHERE DEU.COD_ESD!=4 AND (CURRENT_DATE-DEU.FH_DEUDA_DEA)>=(30*6)
    GROUP BY CLI.RUT_CLE,CLI.DV_CLE,CLI.NOMBRE_CLE,CLI.APATERNO_CLE,DCL.CALLE_DCL,DCL.TELEFONO_DCL
    ORDER BY "DEUDAS" DESC, "MONTO_DEUDA" DESC, "NOMBRE_CLIENTE" ASC
    WITH READ ONLY;

    SELECT * FROM VW_CLIENTES_RECAUDACION;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA3.png" title="hover text">
</p>


4.- Con efectos de publicidad, se ha creado una tabla CLIENTE_OFERTA en la cual en primera instancia se han incluido los clientes registrados en la base de datos, que no registran deudas. Esta tabla permitirá calificar a los clientes destacados, quienes alguna vez han adquirido productos de alguna de las empresas que gestiona PAY NOW, mediante un SCORE, el que se determinará por un cálculo referente a la cantidad de deudas totales y la cantidad de deudas pagadas por el cliente.
PAY NOW desea que se incorpore a la tabla OFERTA_CLIENTE el segmento de clientes que han tenido deudas y que registran al menos una de ellas pagadas. Para ello primeramente debe crear una tabla de paso OFERTA la que contendrá el rut y score (deudas cerradas x 100 / total de deudas), para luego insertar desde OFERTA hacia CLIENTE_OFERTA y ofertar a los clientes adquirir un producto con alguna de las empresas de PAY NOW, con un porcentaje de descuento equivalente a la siguiente tabla: 

| SCORE | OFERTA |
| :---: | :---: |
| 10 a 25 | 10% de descuento |
| 26 a 50 | 15% de descuento |
| 51 a 75 | 20% de descuento |
| 76 o más | 25% de descuento |


    CREATE SEQUENCE SEQ_NUMERO_OFC
    START WITH 1001
    INCREMENT BY 1;
    
    CREATE TABLE OFERTA AS
    SELECT
    SEQ_NUMERO_OFC.NEXTVAL AS "NUMERO_OFC",
    CLI.RUT_CLE AS "RUT_CLE",
    ROUND(((SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE AND COD_ESD=4)*100)/(SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE)) AS "SCORE_OFC",
    CASE
    WHEN ((SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE AND COD_ESD=4)*100)/(SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE) BETWEEN 10 AND 25 THEN 'USTED TIENE UN DESCUENTO DEL 10% EN SU PROXIMA COMPRA CON NUESTRAS EMPRESAS'
    WHEN ((SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE AND COD_ESD=4)*100)/(SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE) BETWEEN 26 AND 50 THEN 'USTED TIENE UN DESCUENTO DEL 15% EN SU PROXIMA COMPRA CON NUESTRAS EMPRESAS'
    WHEN ((SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE AND COD_ESD=4)*100)/(SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE) BETWEEN 51 AND 75 THEN 'USTED TIENE UN DESCUENTO DEL 20% EN SU PROXIMA COMPRA CON NUESTRAS EMPRESAS'
    WHEN ((SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE AND COD_ESD=4)*100)/(SELECT COUNT(*) FROM DEUDA DEU WHERE DEU.RUT_CLE=CLI.RUT_CLE) >=76 THEN 'USTED TIENE UN DESCUENTO DEL 25% EN SU PROXIMA COMPRA CON NUESTRAS EMPRESAS'
    ELSE 'LO INVITAMOS A ADQUIRIR UN PRODUCTO CON NUESTROS CLIENTES'
    END AS "OFERTA_OFC"
    FROM CLIENTE CLI
    WHERE CLI.RUT_CLE IN (SELECT RUT_CLE FROM DEUDA WHERE COD_ESD=4);

    INSERT INTO OFERTA_CLIENTE(NUMERO_OFC,RUT_CLE,SCORE_OFC,OFERTA_OFC)SELECT * FROM OFERTA;

    SELECT * FROM VW_CLIENTES_RECAUDACION;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA4.png" title="hover text">
</p>


5.- A razón de otorgar mayor seguridad en el acceso a datos y objetos de la Base de Datos, se ha decidido generar una estructura de usuarios y privilegios cuales deberá implementar dependiendo de las funciones que cada uno de los funcionarios pueda ejercer sobre la Base de Datos. En base a lo anterior, se ha propuesto la siguiente estructura cual deberá implementar:

5.1.- Crear los siguientes roles con las características indicadas:
|ROL | PRIVILEGIO DE OBJETO |
| :--- | :--- |
| ROL_GESTION | • Consultar datos de la tabla de CLIENTE <br> • Consultar datos de la tabla de NOTIFICACION <br> • Consultar datos de la tabla de DEUDA <br> • Consultas de datos que entrega la Vista <br> VW_CLIENTES_RECAUDACION |
| ROL_MANTENCION | • Consultar y efectuar modificaciones de datos de la tabla de CLIENTE <br> • Consultar y efectuar modificaciones de datos de la tabla de EMPRESA <br> • Consultar datos que entregan las Vistas VW_EMP_SUELDO_COMISION y <br> VW_CLIENTES_RECAUDACION |


--RESPUESTA

    ALTER SESSION SET "_ORACLE_SCRIPT"=TRUE;
    CREATE ROLE ROL_GESTION;
    GRANT SELECT ON CLIENTE TO ROL_GESTION;
    GRANT SELECT ON NOTIFICACION TO ROL_GESTION;
    GRANT SELECT ON DEUDA TO ROL_GESTION;
    GRANT SELECT ON VW_CLIENTES_RECAUDACION TO ROL_GESTION;

    CREATE ROLE ROL_MANTENCION;
    GRANT SELECT,UPDATE ON CLIENTE TO ROL_MANTENCION;
    GRANT SELECT,UPDATE ON EMPRESA TO ROL_MANTENCION;
    GRANT SELECT ON VW_EMP_SUELDO_COMISION TO ROL_MANTENCION;
    GRANT SELECT ON VW_CLIENTES_RECAUDACION TO ROL_MANTENCION;

    SELECT * FROM DBA_ROLES;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA5.1.png" title="hover text">
</p>


5.2.- Crear los siguientes usuarios de acuerdo a las siguientes especificaciones:

| USUARIO | ROL | PRIVILEGIO DE OBJETO | PRIVILEGIO DE SISTEMA |
| :--- | :--- | :--- | :--- |
| USR_EJECUTIVO | • ROL_CONSULTA <br> • CONNECT | • Consultar datos de la tabla de EMPRESA | |	
| USR_DESARROLLO | • CONNECT <br> • RESOURCE <br> • ROL_MANTENCION | • Consultar y efectuar modificaciones de datos de la tabla de USUARIO. <br> • Consultar datos de la tabla de DEUDA | Crear Vistas y Vistas Materializadas |
| USR_GERENCIA | • CONNECT | • Consultar datos que entregan las vistas VW_CLIENTES_RECAUDACION y VW_STOCK_NOTIFICADO | |


--RESPUESTA

    ALTER SESSION SET "_ORACLE_SCRIPT"=TRUE;
    CREATE USER USR_EJECUTIVO IDENTIFIED BY "123";
    GRANT ROL_GESTION TO USR_EJECUTIVO;
    GRANT CONNECT TO USR_EJECUTIVO;
    GRANT SELECT ON EMPRESA TO USR_EJECUTIVO;

    CREATE USER USR_DESARROLLO IDENTIFIED BY "123";
    GRANT CONNECT,RESOURCE TO USR_DESARROLLO;
    GRANT ROL_MANTENCION TO USR_DESARROLLO;
    GRANT SELECT,UPDATE ON USUARIO TO USR_DESARROLLO;
    GRANT SELECT ON DEUDA TO USR_DESARROLLO;
    GRANT CREATE VIEW,CREATE MATERIALIZED VIEW TO USR_DESARROLLO;

    CREATE USER USR_GERENCIA IDENTIFIED BY "123";
    GRANT CONNECT TO USR_GERENCIA;
    GRANT SELECT ON VW_CLIENTES_RECAUDACION TO USR_GERENCIA;
    GRANT SELECT ON VW_STOCK_NOTIFICADO TO USR_GERENCIA;

    SELECT * FROM ALL_USERS;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA5.2.png" title="hover text">
</p>


5.3.- Crear sinónimos para que cualquier usuario de base de datos que tenga privilegios sobre las tablas NOTIFICACION, CLIENTE y EMPRESA sin tener que accederlas usando owner.nombre_tabla sino que usando sólo el nombre la tabla.


--RESPUESTA

    CREATE SYNONYM NOTIF FOR NOTIFICACION;
    GRANT SELECT ON NOTIF TO USR_EJECUTIVO;

    CREATE SYNONYM CLI FOR CLIENTE;
    GRANT SELECT ON CLI TO USR_EJECUTIVO;
    GRANT SELECT,UPDATE ON CLI TO USR_DESARROLLO;

    CREATE SYNONYM EMP FOR EMPRESA;
    GRANT SELECT,UPDATE ON EMP TO USR_DESARROLLO;
    GRANT SELECT ON EMP TO USR_EJECUTIVO;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA5.3.png" title="hover text">
</p>


5.4.- Crear sinónimos para que sólo los usuarios USR_EJECUTIVO y USR_DESARROLLO accedan a la vista VW_CLIENTES_RECAUDACION sin tener que usar owner.nombre_vista sino que usando sólo el nombre de la vista.


--RESPUESTA

    CREATE SYNONYM V_CLI_REC_ED FOR VW_CLIENTES_RECAUDACION;
    GRANT SELECT ON V_CLI_REC_ED TO USR_EJECUTIVO,USR_DESARROLLO;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA5.4.png" title="hover text">
</p>


5.5.-Crear sinónimo para que sólo el usuario USR_GERENCIA acceda a las vista VW_STOCK_NOTIFICADO  y VW_CLIENTES_RECAUDACION  sin tener que usar owner.nombre_vista sino que usando sólo el nombre de la vista.


--RESPUESTA

    CREATE SYNONYM V_STOCK_NOTIF FOR VW_STOCK_NOTIFICADO;
    GRANT SELECT ON V_STOCK_NOTIF TO USR_GERENCIA;
    CREATE SYNONYM V_CLI_REC_GE FOR VW_CLIENTES_RECAUDACION;
    GRANT SELECT ON V_CLI_REC_GE TO USR_GERENCIA;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA5.5.png" title="hover text">
</p>


6.- Se ha detectado una lentitud en la respuesta de la Base de Datos, a lo cual se realizó un análisis para detectar la problemática, y se ha deducido que hay dos consultas que demoran la respuesta y el proceso de la Base de Datos, cual afecta en la gestión de las cobranzas diariamente. El resultado del análisis detecto lo siguiente:
6.1.- El informe del ranking mensual de las comunas riesgosas presenta un problema de lentitud y al obtener los datos ejecutando la sentencia y su plan de ejecución, se observa que tabla DEUDA se está recorriendo completa para el análisis de los datos. La sentencia ejecutada es la siguiente:

    SELECT 
    COM.NOMBRE_COM "COMUNA",
    COUNT(*) "CANT. CLIENTES CON DEUDA",
    TO_CHAR(AVG(DEU.MONTO_DEA),'$999G999G999') "PROMEDIO DEUDA",
    TO_CHAR(MIN(DEU.MONTO_DEA),'$999G999G999') "MONTO MINIMO",
    TO_CHAR(MAX(DEU.MONTO_DEA),'$999G999G999') "MONTO MAXIMO"
    FROM DEUDA DEU
    JOIN CLIENTE CLI ON (DEU.RUT_CLE = CLI.RUT_CLE)
    JOIN DIRECCION_CLIENTE DI ON (CLI.RUT_CLE = DI.RUT_CLE)
    JOIN COMUNA COM ON (DI.ID_COM = COM.ID_COM)
    WHERE 
    DEU.COD_ESD <> DEU.FH_DEUDA_DEA BETWEEN TO_DATE('2018/08/20','YYYY/MM/DD') - 90 AND TO_DATE('2018/08/20','YYYY/MM/DD')
    GROUP BY COM.NOMBRE_COM
    HAVING COUNT(*) >= 3;

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA6.1.1.png" title="hover text">
</p>

La solución fue crear un índice asociado a la tabla DEUDA y con esto se logró que el acceso ahora sea BY INDEX ROWID usando el índice que se creó. Esto redujo el tiempo de respuesta de la sentencia.
Sin embargo, un usuario por error eliminó este índice por lo que es de urgencia que Ud. lo vuelva a crear para lograr que el acceso a la tabla DEUDA sea usando el índice IDX_DEUDA como se muestra en el plan de ejecución del ejemplo:

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA6.1.2.png" title="hover text">
</p>


--RESPUESTA

    CREATE INDEX IDX_DEUDA ON DEUDA(FH_DEUDA_DEA);

6.2.- El otro informe que ha causado problemas, refiere a la cantidad de clientes que se tienen por región, el cual consulta por el nombre de la región de la cual se requieren los datos. En el ejemplo, se obtienen los datos de los clientes relacionados a la Región  Metropolitana de Santiago, y al obtener el plan de ejecución se puede observar que el acceso a la tabla REGION está siendo accedida en modo FULL.

    SELECT 
    CO.NOMBRE_COM "COMUNA",
    COUNT(DC.RUT_CLE) "CANTIDAD CLIENTES"
    FROM COMUNA CO
    LEFT JOIN DIRECCION_CLIENTE DC ON CO.ID_COM = DC.ID_COM
    WHERE CO.ID_PROV IN (
    SELECT ID_PROV 
    FROM PROVINCIA  
    WHERE 
    ID_REG IN (
    SELECT ID_REG 
    FROM REGION 
    WHERE 
    trim(UPPER(NOMBRE_REG)) = trim(UPPER('Región Metropolitana de Santiago'))))
    GROUP BY CO.NOMBRE_COM

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA6.2.1.png" title="hover text">
</p>

Efectuadas algunas pruebas, los mejores tiempos de respuestas de la consulta se lograron creando el índice IDX_REGION asociado a la tabla REGION ya que de esta forma la tabla es accedida BY INDEX ROWID según el nuevo plan de ejecución.  Por esta razón, se requiere que Ud. cree en forma definitiva el índice IDX_REGION para que la sentencia que obtiene la cantidad de clientes que se tienen por el nombre de la región sea ejecutada usando el nuevo índice según se muestra en el ejemplo:

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_COBRANZA_SQL/IMAGENES/RESPUESTA6.2.2.png" title="hover text">
</p>


--RESPUESTA

    CREATE INDEX IDX_REGION ON REGION(TRIM(UPPER(NOMBRE_REG)));
