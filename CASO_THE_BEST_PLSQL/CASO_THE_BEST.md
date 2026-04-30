# Optimización Procesos del Sistema Informático de Clientes y Transacciones de la empresa de Retail “THE BEST”

<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/LOGO.jpg" width="350" title="hover text">
</p>

THE BEST es una empresa de Retail perteneciente al Holding Chileno GRUPO TERRACHILE S.A que se fundó el año el año 2010 y en el año 2017 creó THE BEST y que a la fecha de hoy cuenta con sucursales en todas las regiones del país. Su éxito se debe a las estrategias innovadoras que se han implementado en estos años beneficiando a sus clientes en compras, avances en efectivo y súper avances con tasas de interés más atractivas que las ofrecidas por las otras empresas del mismo rubro y entidades bancarias tradicionales. 
Para poder optar a los avances en efectivo y/o súper avances, la persona debe poseer la tarjeta THE BEST, con la cual también puede efectuar compras en cuotas en las diferentes tiendas que posee el Retail. Cuando una persona solicita la tarjeta THE BEST, se completa un formulario con los siguientes datos personales del cliente:
•	Run
•	Nombre completo
•	Fecha de nacimiento
•	Correo (que es opcional)
•	Dirección completa (Incluyendo región y provincia) en la que vive
•	Profesión u ocupación 
El cupo que se le asigna al cliente para que pueda efectuar compras, avances y súper avances tiene relación directa a la renta que percibe. Por esta razón, según corresponda, debe presentar lo siguiente:
•	Trabajadores dependientes: deben presentar un certificado que indique los datos de la institución donde trabajan, años de antigüedad y el promedio de su sueldo mensual.
•	Trabajadores independientes: deben presentar sus boletas de honorarios que acrediten las labores mensuales por las cuales percibe un sueldo en los últimos 2 años (a la fecha de inscripción como cliente). De acuerdo al monto total de las remuneraciones percibidas en los últimos 2 años, el Banco calcula un promedio mensual de renta para estos clientes.
•	Pensionados y Tercera Edad: se les solicita certificado que acredite renta mensual de la pensión que percibe de los últimos 12 meses. A partir de las 12 últimas rentas acreditadas el Banco calcula el promedio de renta mensual del cliente.

Al momento de inscribirse, a cada cliente se le entrega una tarjeta de la empresa para que pueda efectuar compras, solicitar avances en efectivo o solicitar súper avances en cuotas. El cliente puede tener más de una tarjeta si lo desea. 
Al ser cliente de THE BEST, la persona puede optar por cualquiera de los otros productos que la empresa de Retail dispone para sus clientes. Cualquiera de ellos se debe solicitar personalmente en el área financiera de las sucursales que posee la empresa:

| Identificación del Producto | Nombre del Producto | Tasa de Interés del Producto | Número Máximo de Cuotas en las que puede solicitar el Crédito |
| :---: | :---: | :---: | :---: |
| 1 | Tarjeta THE BEST | | |
| 2 | Crédito de Consumo | 0,5 | 72 |
| 3 | Crédito Automotriz | 0,4 | 60 |
| 4 | Crédito de Emergencia | 0,35 | 48 |
| 5 | SOAP | | |
| 6 | Seguro de Vida | | |
| 7 | Seguro de Salud	| | |
| 8 | Seguro de Hogar | | |

Cuando se le entrega la tarjeta THE BEST al cliente se le hace firmar un documento en el que se le informa el cupo máximo (en dinero) para tendrá para efectuar compras, avances en efectivo o súper avances. El cupo de compras asignado incluye el monto destinado para avances en efectivo y que corresponde al 40% del cupo total de compras. Para los súper avances al cliente se le asigna un cupo especial ya que es administrado como si fuera un crédito de consumo, pero con un monto máximo a solicitar menor.
La tasa de interés para cualquier transacción efectuada con la tarjeta THE BEST está definida de acuerdo a lo siguiente:

| Identificación del tipo de Transacción | Nombre del tipo de Transacción | Tasa de Interés por cuota | Nro. Máximo Cuotas en que se puede solicitar |
| :---: | :---: | :---: | :---: |
| 101 | Compras Tiendas del Retail o Asociadas | 0,05 | 48 |
| 102 | Avance en Efectivo | 0,05 | 24 |
| 103 | Súper Avance en Efectivo | 0,1 | 36 |

A un cliente se le pueden entregar un máximo de 3 tarjetas adicionales cada una de ellas con un número diferente. Para que al cliente se le entregue más de una tarjeta adicional debe poseer un salario líquido mensual igual o superior a los $2.000.000 mensuales. Cada vez que un cliente utiliza su tarjeta para efectuar una transacción en alguna sucursal (física o virtual) queda registrada la siguiente información: 
•	Identificación de la sucursal en la que el cliente efectuó la compra, el avance o súper avance en dinero
•	Región, provincia y comuna a la que pertenece la sucursal en la que el cliente efectuó la transacción
•	Número de la tarjeta con la que el cliente efectuó la transacción
•	Fecha de la transacción
•	Tipo de transacción que efectuó (compra, avance o súper avance)
•	Monto de la transacción
•	Número de cuotas a pagar
•	Valor de cada cuota (con la tasa de interés aplicada)
•	Fecha de vencimiento de cada cuota
•	Monto total la transacción (con la tasa de interés aplicada)
El cliente tiene un máximo de 5 días, desde la fecha de la transacción, para anula una compra. Los avances y súper avances en dinero no se pueden anular. 
En los últimos seis meses el THE BEST se ha posicionado como la más exitosa en su rubro a lo largo del país. Esto ha permitido efectuar una proyección y se estima que al finalizar el año contará con más de cinco millones de clientes. Esta nueva posición de THE BEST en el mercado nacional tendrá directa relación con el aumento de las transacciones diarias que los clientes efectúan en todas las sucursales de la empresa.
A esto también se suma la nueva Ley de Operaciones de Avances y Súper Avances en dinero que entrará en vigencia en el mes de septiembre de este año y que obliga a todas las empresas del Retail a aportar un porcentaje de las ganancias de este tipo de transacciones y que estarán enfocados a la implementación de proyectos de formación de capital humano que permita insertar a Chile en la sociedad del conocimiento, dando así un impulso definitivo al desarrollo económico, social y cultural de nuestro país.  Por lo tanto, las empresas de este rubro deberán enviar mensualmente a la Superintendencia de Bancos e Instituciones Financieras de Chile (SBIF) el detalle de todas las transacciones efectuadas en el mes y el monto que por cada una de ellas serán el aporte que administrará por la SBIF.
Para ambos desafíos que THE BEST debe enfrentar, se requiere crear y rediseñar algunos de los procesos del Sistema Informático para lograr una gestión eficiente y eficaz de la información de sus clientes y las transacciones que los clientes efectúan con la tarjeta THE BEST.
Para efectuar este trabajo, THE BEST lo ha contratado a Ud. y en reunión efectuada con el cliente se definieron los hitos que van a ser consideraros cada etapa de este proyecto y las fechas de entregas de cada una de ellas de acuerdo a la urgencia de los requerimientos a resolver. 

# RESUMEN REQUERIMIENTOS A RESOLVER
En esta primera etapa se deben resolver los siguientes requerimientos:
1.-La empresa de retail implementará el nuevo Programa de Puntos CIRCULO THE BEST orientado a los clientes que utilicen su tarjeta para efectuar compras, avances y/o súper avances en dinero. Por lo tanto, se requiere que cada vez que un cliente utilice su tarjeta para efectuar cualquier transacción, se registre automáticamente los puntos que obtuvo. Para obtener los puntos, se hace la división del monto de la transacción por 10000 y luego multiplicados por 250.

--RESPUESTA

    CREATE OR REPLACE TRIGGER TGR_PUNTOS
    AFTER INSERT OR UPDATE OR DELETE ON TRANSACCION_TARJETA_CLIENTE
    FOR EACH ROW
    DECLARE
    BEGIN

    IF INSERTING THEN
    UPDATE PUNTOS_CIRCULO_THE_BEST
    SET TOTAL_PUNTOS = TOTAL_PUNTOS+(250*TRUNC(:NEW.MONTO_TOTAL_TRANSACCION/10000)),
    FECHA_ACTUALIZACION = SYSDATE
    WHERE NRO_TARJETA=:NEW.NRO_TARJETA;
    IF SQL%ROWCOUNT = 0 THEN
    INSERT INTO PUNTOS_CIRCULO_THE_BEST VALUES(:NEW.NRO_TARJETA,250*TRUNC(:NEW.MONTO_TOTAL_TRANSACCION/10000),SYSDATE);
    END IF;
    END IF;

    IF UPDATING THEN

    IF :OLD.MONTO_TOTAL_TRANSACCION > :NEW.MONTO_TOTAL_TRANSACCION THEN
    UPDATE PUNTOS_CIRCULO_THE_BEST
    SET TOTAL_PUNTOS = TOTAL_PUNTOS-((250*TRUNC(:OLD.MONTO_TOTAL_TRANSACCION/10000))-(250*TRUNC(:NEW.MONTO_TOTAL_TRANSACCION/   10000))),
    FECHA_ACTUALIZACION = SYSDATE
    WHERE NRO_TARJETA=:NEW.NRO_TARJETA;
    END IF;

    IF :OLD.MONTO_TOTAL_TRANSACCION < :NEW.MONTO_TOTAL_TRANSACCION THEN
    UPDATE PUNTOS_CIRCULO_THE_BEST
    SET TOTAL_PUNTOS = TOTAL_PUNTOS+((250*TRUNC(:NEW.MONTO_TOTAL_TRANSACCION/10000))-(250*TRUNC(:OLD.MONTO_TOTAL_TRANSACCION/   10000))),
    FECHA_ACTUALIZACION = SYSDATE
    WHERE NRO_TARJETA=:OLD.NRO_TARJETA;
    END IF;

    END IF;

    IF DELETING THEN
    UPDATE PUNTOS_CIRCULO_THE_BEST
    SET TOTAL_PUNTOS = TOTAL_PUNTOS-(250*TRUNC(:OLD.MONTO_TOTAL_TRANSACCION/10000)),
    FECHA_ACTUALIZACION = SYSDATE
    WHERE NRO_TARJETA=:OLD.NRO_TARJETA;
    END IF;

    END;

--PRUEBAS

    INSERT INTO TRANSACCION_TARJETA_CLIENTE VALUES(32723552593,1004,'27/02/26',537600,12,591360,103,3011);
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/RESPUESTA1.1.png" title="hover text">
</p>

    UPDATE TRANSACCION_TARJETA_CLIENTE SET
    MONTO_TOTAL_TRANSACCION = 700000
    WHERE NRO_TARJETA=32723552593 AND NRO_TRANSACCION=1004;
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/RESPUESTA1.2.png" title="hover text">
</p>

    DELETE FROM TRANSACCION_TARJETA_CLIENTE
    WHERE NRO_TARJETA=32723552593 AND NRO_TRANSACCION=1004;
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/RESPUESTA1.3.png" title="hover text">
</p>


2.-Se requieren contar con un proceso que diariamente a las 23:00 horas actualice las fotografías que los clientes han entregado para completar sus antecedentes en el Sistema.

--RESPUESTA

    CREATE OR REPLACE DIRECTORY FOTOS_CLIENTE AS 'C:\fotos_clientes';

--Realizar este grant desde un usuario con privilegios mas elevados.

    GRANT READ, WRITE ON DIRECTORY FOTOS_CLIENTE TO BEST;

--Proceso para insertar errores

    CREATE OR REPLACE PROCEDURE SP_ERRORES(P_RUTINA VARCHAR, P_DESCRIPCION VARCHAR)IS
    BEGIN
        INSERT INTO ERROR_AVAN_SAVAN_MENSUALES VALUES(SEQ_ERROR.NEXTVAL,P_RUTINA,P_DESCRIPCION);
    END SP_ERRORES;

--ITEM 2

--INSERCION DE FOTOGRAFIAS

    SET SERVEROUTPUT ON;

    CREATE OR REPLACE PROCEDURE PRC_ACTUALIZAR_FOTOS IS
    CURSOR C_CLIENTE IS
    (SELECT
    NUMRUN
    FROM
    CLIENTE
    );
    RUT_CLIENTE CLIENTE.NUMRUN%TYPE;
    V_FOTO BLOB;
    V_CARPETA BFILE;
    V_CODE NUMBER(6);
    V_MENSAJE VARCHAR2(200);
    BEGIN
    OPEN C_CLIENTE;
    LOOP
    FETCH C_CLIENTE INTO RUT_CLIENTE;
    EXIT WHEN C_CLIENTE%NOTFOUND;
    BEGIN

    UPDATE CLIENTE
    SET
    FOTO = EMPTY_BLOB
    WHERE
    RUT_CLIENTE = NUMRUN
    RETURNING FOTO INTO V_FOTO;

    V_CARPETA := BFILENAME('FOTOS_CLIENTE', RUT_CLIENTE || '.jpg');
    DBMS_LOB.OPEN(V_CARPETA, DBMS_LOB.LOB_READONLY);
    DBMS_LOB.LOADFROMFILE(V_FOTO, V_CARPETA, DBMS_LOB.GETLENGTH(V_CARPETA));
    DBMS_LOB.CLOSE(V_CARPETA);
    EXCEPTION
    WHEN OTHERS THEN
    V_MENSAJE := SQLERRM;
    SP_ERRORES('ALMACENAMIENTO FOTOGRAFIA CON EL RUT: '||RUT_CLIENTE, SQLERRM);
    END;
    END LOOP;
    CLOSE C_CLIENTE;
    END;

--CREAMOS UN JOB PARA QUE SE INICIE TODOS LOS DIAS A LAS 23:00

    BEGIN
        DBMS_SCHEDULER.CREATE_JOB(
        JOB_NAME =>'ACTUALIZAR_FOTOGRAFIAS',
        JOB_TYPE =>'STORED_PROCEDURE',
        JOB_ACTION =>'BEST.PRC_ACTUALIZAR_FOTOS',
        --REPEAT_INTERVAL =>'FREQ=MINUTELY;INTERVAL=1',
        REPEAT_INTERVAL =>'FREQ=DAILY;BYHOUR=23;BYMINUTE=0;BYSECOND=0',
        AUTO_DROP=>FALSE,
        ENABLED =>TRUE,
        COMMENTS => 'ACTULIZA LAS FOTOS DE LOS CLIENTES'
        );
    END;

--EJECUTAMOS MANUALMENTE PARA COMPROBAR

    EXEC PRC_ACTUALIZAR_FOTOS;
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/RESPUESTA2.png" title="hover text">
</p>

3.-Se requiere un proceso que mensualmente genere la información de los avances y súper avances en dinero que fueron solicitados durante el mes y que debe ser enviada a la SBIF. Este proceso se deberá ejecutar automáticamente el día 06 de cada mes y debe permitir saber información detallada de los avances y súper avances que fueron solicitados en el mes anterior a la fecha de ejecución. Por ejemplo, si el proceso se ejecuta el 06 de febrero del 2019, se deberá generar la información del mes de enero del 2019.

--RESPUESTA

    CREATE OR REPLACE PROCEDURE PRC_INFORME_AVANCES_SUPERS IS
    CURSOR C_DETALLE IS
    SELECT
    TO_CHAR(SYSDATE,'MM-YYYY')AS "MES_ANNO_PROCESO",
    SRE.ID_SUCURSAL AS "ID_SUCURSAL",
    REG.NOMBRE_REGION AS "REGION",
    PRO.NOMBRE_PROVINCIA AS "PROVINCIA",
    CO.NOMBRE_COMUNA AS "COMUNA",
    TTC.FECHA_TRANSACCION AS "FECHA_TRANSACCION",
    TTC.NRO_TRANSACCION AS "NRO_TRANSACCION",
    TAC.NUMRUN||'-'||CLI.DVRUN AS "RUN_CLIENTE",
    TTC.NRO_TARJETA AS "NRO_TARJETA",
    CLI.PNOMBRE||' '||CLI.APPATERNO||' '||CLI.APMATERNO AS "NOMBRE_CLIENTE",
    TTC.MONTO_TRANSACCION AS "MONTO_SOLICITADO",
    TTC.MONTO_TOTAL_TRANSACCION AS "MONTO_TOTAL_AVAN_SAVAN",
    TTC.TOTAL_CUOTAS_TRANSACCION AS "NRO_TOTAL_CUOTAS",
    (TTC.FECHA_TRANSACCION+30) AS "VENCIMIENTO_PRIMERA_CUOTA",
    (TTC.FECHA_TRANSACCION+(30*TTC.TOTAL_CUOTAS_TRANSACCION)) AS "VENCIMIENTO_ULTIMA_CUOTA",
    (TTC.MONTO_TOTAL_TRANSACCION-TTC.MONTO_TRANSACCION)*0.1 AS "MONTO_CORRESPONDE_SBIF"
    FROM TRANSACCION_TARJETA_CLIENTE TTC
    INNER JOIN SUCURSAL_RETAIL SRE ON SRE.ID_SUCURSAL=TTC.ID_SUCURSAL
    INNER JOIN REGION REG ON REG.COD_REGION=SRE.COD_REGION
    INNER JOIN PROVINCIA PRO ON PRO.COD_PROVINCIA = SRE.COD_PROVINCIA AND PRO.COD_REGION=SRE.COD_REGION
    INNER JOIN COMUNA CO ON CO.COD_COMUNA=SRE.COD_COMUNA AND CO.COD_REGION=SRE.COD_REGION AND CO.COD_PROVINCIA = SRE.COD_PROVINCIA
    INNER JOIN TARJETA_CLIENTE TAC ON TAC.NRO_TARJETA=TTC.NRO_TARJETA
    INNER JOIN CLIENTE CLI ON CLI.NUMRUN=TAC.NUMRUN
    --WHERE TO_CHAR(TTC.FECHA_TRANSACCION,'MM-YYYY')=TO_CHAR(ADD_MONTHS(SYSDATE,-1),'MM-YYYY') AND TTC.COD_TPTRAN_TARJETA != 101;
    --PARA FINES DE OBTENER DATOS SE USO ESTE PARAMETRO.
    WHERE TO_CHAR(TTC.FECHA_TRANSACCION,'MM-YYYY')='01-2019' AND TTC.COD_TPTRAN_TARJETA != 101;
    REG_DETALLE C_DETALLE%ROWTYPE;
    V_CORRELATIVO	NUMBER(6,0);
    V_MES_ANNO_PROCESO	VARCHAR2(7 BYTE);
    V_ID_SUCURSAL	NUMBER(5,0);
    V_REGION	VARCHAR2(50 BYTE);
    V_PROVINCIA	VARCHAR2(50 BYTE);
    V_COMUNA	VARCHAR2(50 BYTE);
    V_FECHA_TRANSACCION	DATE;
    V_NRO_TRANSACCION	NUMBER(10,0);
    V_RUN_CLIENTE	VARCHAR2(12 BYTE);
    V_NRO_TARJETA	NUMBER(30,0);
    V_NOMBRE_CLIENTE	VARCHAR2(50 BYTE);
    V_MONTO_SOLICITADO	NUMBER(15,0);
    V_MONTO_TOTAL_AVAN_SAVAN	NUMBER(15,0);
    V_NRO_TOTAL_CUOTAS	NUMBER(2,0);
    V_VENCIMIENTO_PRIMERA_CUOTA	DATE;
    V_VENCIMIENTO_ULTIMA_CUOTA	DATE;
    V_MONTO_CORRESPONDE_SBIF	NUMBER(10,0);
    BEGIN
    OPEN C_DETALLE;
    LOOP
    FETCH C_DETALLE INTO REG_DETALLE;
    EXIT WHEN C_DETALLE%NOTFOUND;
    V_MES_ANNO_PROCESO := REG_DETALLE.MES_ANNO_PROCESO;
    V_ID_SUCURSAL := REG_DETALLE.ID_SUCURSAL;
    V_REGION := REG_DETALLE.REGION;
    V_PROVINCIA := REG_DETALLE.PROVINCIA;
    V_COMUNA := REG_DETALLE.COMUNA;
    V_FECHA_TRANSACCION := REG_DETALLE.FECHA_TRANSACCION;
    V_NRO_TRANSACCION := REG_DETALLE.NRO_TRANSACCION;
    V_RUN_CLIENTE := REG_DETALLE.RUN_CLIENTE;
    V_NRO_TARJETA := REG_DETALLE.NRO_TARJETA;
    V_NOMBRE_CLIENTE := REG_DETALLE.NOMBRE_CLIENTE;
    V_MONTO_SOLICITADO := REG_DETALLE.MONTO_SOLICITADO;
    V_MONTO_TOTAL_AVAN_SAVAN := REG_DETALLE.MONTO_TOTAL_AVAN_SAVAN;
    V_NRO_TOTAL_CUOTAS := REG_DETALLE.NRO_TOTAL_CUOTAS;
    V_VENCIMIENTO_PRIMERA_CUOTA := REG_DETALLE.VENCIMIENTO_PRIMERA_CUOTA;
    V_VENCIMIENTO_ULTIMA_CUOTA := REG_DETALLE.VENCIMIENTO_ULTIMA_CUOTA;
    V_MONTO_CORRESPONDE_SBIF := REG_DETALLE.MONTO_CORRESPONDE_SBIF;
    INSERT INTO DETALLE_AVAN_SAVAN_MENSUALES VALUES(SEQ_DET_AVAN_SAVAN_MENSUALES.NEXTVAL,V_MES_ANNO_PROCESO,V_ID_SUCURSAL,V_REGION,V_PROVINCIA,V_COMUNA,V_FECHA_TRANSACCION,V_NRO_TRANSACCION,V_RUN_CLIENTE,V_NRO_TARJETA,V_NOMBRE_CLIENTE,V_MONTO_SOLICITADO,V_MONTO_TOTAL_AVAN_SAVAN,V_NRO_TOTAL_CUOTAS,V_VENCIMIENTO_PRIMERA_CUOTA,V_VENCIMIENTO_ULTIMA_CUOTA,V_MONTO_CORRESPONDE_SBIF);
    INSERT INTO RESUMEN_AVAN_SAVAN_MENSUALES VALUES(SEQ_RES_AVAN_SAVAN_MENSUALES.NEXTVAL,V_MES_ANNO_PROCESO,V_FECHA_TRANSACCION,V_MONTO_SOLICITADO,V_MONTO_TOTAL_AVAN_SAVAN,V_MONTO_CORRESPONDE_SBIF);
    END LOOP;
    CLOSE C_DETALLE;
    END;

--CREAMOS UN JOB QUE SE EJECUTE EL DIA PRIMERO DE CADA MES

    BEGIN
        DBMS_SCHEDULER.CREATE_JOB(
        JOB_NAME =>'CREAR_INFORME_MENSUAL',
        JOB_TYPE =>'STORED_PROCEDURE',
        JOB_ACTION =>'BEST.PRC_INFORME_AVANCES_SUPERS',
        --REPEAT_INTERVAL =>'FREQ=MINUTELY;INTERVAL=1',
        REPEAT_INTERVAL =>'FREQ=MONTHLY; BYMONTHDAY=1; BYHOUR=0; BYMINUTE=0; BYSECOND=0',
        AUTO_DROP=>FALSE,
        ENABLED =>TRUE,
        COMMENTS => 'SE REALIZA EL INFORME MENSUAL DE LOS AVANCES Y SUPERS'
        );
    END;

--EJECUTAMOS MANUALMENTE PARA COMPROBAR

    EXEC PRC_INFORME_AVANCES_SUPERS;

DETALLE_AVAN_SAVAN_MENSUALES
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/RESPUESTA3.1.png" title="hover text">
</p>

RESUMEN_AVAN_SAVAN_MENSUALES
<p align="center">
  <img src="https://raw.githubusercontent.com/matiassanmartins/ORACLESQL/refs/heads/main/CASO_THE_BEST_PLSQL/IMAGENES/RESPUESTA3.2.png" title="hover text">
</p>
