---
title: "Conector de hello DB2 aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general del conector de DB2 con parámetros de la API de REST"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Empezar a trabajar con el conector de DB2 Hola
Conector de Microsoft para DB2 conecta tooresources Logic Apps almacenados en una base de datos de IBM DB2. Este conector incluye un toocommunicate de cliente de Microsoft con los equipos de servidor DB2 remotos a través de una red TCP/IP. Esto incluye las bases de datos en la nube, como IBM Bluemix dashDB o IBM DB2 para Windows que se ejecuta en la virtualización de Azure y un bases de datos mediante la puerta de enlace de datos de Hola de local a local. Vea hello [admite lista](connectors-create-api-db2.md#supported-db2-platforms-and-versions) de plataformas IBM DB2 y las versiones (en este tema).

Conector de Hello DB2 admite hello las siguientes operaciones de base de datos:

* Mostrar tablas de base de datos
* Leer una fila mediante SELECT
* Leer todas las filas mediante SELECT
* Agregar una fila mediante INSERT
* Modificar una fila mediante UPDATE
* Quitar una fila mediante DELETE

Este tema muestra cómo toouse conector de hello en un tooprocess de aplicación lógica la base de las operaciones de datos.

toolearn más información acerca de las aplicaciones lógicas, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Acciones disponibles
Conector de Hello DB2 admite Hola siguientes acciones de aplicación lógica:

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Enumeración de tablas
Crear una aplicación de la lógica para cualquier operación consta de varios pasos que se realiza a través del portal de Microsoft Azure Hola.

Dentro de la aplicación de la lógica de hello, puede agregar las tablas de toolist de acción en una base de datos DB2. Hello acción indica Hola conector tooprocess DB2 schema, instrucción, como `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `Db2getTables`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, establezca hello **Intervalo** tootype **7**.  
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba `db2` en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **DB2 - Get tablas (versión preliminar)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. Hola **DB2 - Get tablas** panel de configuración, seleccione **casilla** tooenable **conectar a través de puerta de enlace de datos local**. Observe que cambia configuración de Hola de nube local tooon.
   
   * Escriba el valor de **Server**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `ibmserver01:50000`.
   * Escriba un valor para **Base de datos**. Por ejemplo, escriba `nwind`.
   * Seleccione un valor para **Autenticación**. Por ejemplo, seleccione **Básico**.
   * Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `db2admin`.
   * Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
   * Seleccione el valor para **Puerta de enlace**. Por ejemplo, seleccione **datagateway01**.
7. Seleccione **Crear** y, a continuación, seleccione **Guardar**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. Hola **Db2getTables** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
9. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_tables**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir una lista de tablas.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Crear conexiones de Hola
Este conector es compatible con las conexiones toodatabases hospedado local y en la nube de hello utilizando Hola propiedades de conexión siguientes. 

| Propiedad | Description |
| --- | --- |
| Servidor |Obligatorio. Acepta un valor de cadena que representa una dirección TCP/IP o alias en formato IPv4 o IPv6 seguido de un número de puerto TCP/IP (delimitado por dos puntos). |
| Base de datos |Obligatorio. Acepta un valor de cadena que representa un nombre de base de datos relacional de DRDA (RDBNAM). DB2 para z/OS acepta una cadena de 16 bytes (la base de datos se conoce como una base de datos IBM DB2 para la ubicación z/OS). DB2 para i5/OS acepta una cadena de 18 bytes (la base de datos se conoce como una base de datos IBM DB2 para la base de datos relacional i). DB2 para LUW acepta una cadena de 8 bytes. |
| Autenticación |Opcional. Acepta un valor de elemento de lista que puede ser Basic o Windows (kerberos). |
| Nombre de usuario |Obligatorio. Acepta un valor de cadena. DB2 para z/OS acepta una cadena de 8 bytes. DB2 para i acepta una cadena de 10 bytes. DB2 para Linux o UNIX acepta una cadena de 8 bytes. DB2 para Windows acepta una cadena de 30 bytes. |
| Contraseña |Obligatorio. Acepta un valor de cadena. |
| Puerta de enlace |Necesario. Acepta un valor de elemento de lista, que representa Hola local datos definido de la puerta de enlace tooLogic aplicaciones en el grupo de almacenamiento de Hola. |

## <a name="create-hello-on-premises-gateway-connection"></a>Crear conexiones de puerta de enlace de hello local
Este conector puede tener acceso a una base de datos DB2 local mediante la puerta de enlace de hello en local. Consulte los temas sobre puertas de enlace para más información. 

1. Hola **puertas de enlace** panel de configuración, seleccione **casilla** tooenable **conectar a través de puerta de enlace**. Observe que cambia configuración de Hola de nube local tooon.
2. Escriba el valor de **Server**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `ibmserver01:50000`.
3. Escriba un valor para **Base de datos**. Por ejemplo, escriba `nwind`.
4. Seleccione un valor para **Autenticación**. Por ejemplo, seleccione **Básico**.
5. Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `db2admin`.
6. Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
7. Seleccione el valor para **Puerta de enlace**. Por ejemplo, seleccione **datagateway01**.
8. Seleccione **crear** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Crear la conexión de hello en la nube
Este conector puede tener acceso a una base de datos DB2 en la nube. 

1. Hola **puertas de enlace** panel de configuración, deje hello **casilla** deshabilitado (los) **conectar a través de puerta de enlace**. 
2. Escriba un valor para **Nombre de conexión**. Por ejemplo, escriba `hisdemo2`.
3. Escriba el valor de **nombre del servidor DB2**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `hisdemo2.cloudapp.net:50000`.
4. Escriba un valor para **Nombre de la base de datos DB2**. Por ejemplo, escriba `nwind`.
5. Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `db2admin`.
6. Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
7. Seleccione **crear** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Recuperar todas las filas mediante SELECT
Puede definir un toofetch de acción de aplicación lógica de todas las filas de una tabla de DB2. Esto indica Hola conector tooprocess una instrucción SELECT de DB2, como `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `Db2getRows`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba `db2` en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **DB2 - Get filas (versión preliminar)**.
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**.
7. Hola **conexiones** panel de configuración, seleccione **crear nuevo**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. Hola **puertas de enlace** panel de configuración, deje hello **casilla** deshabilitado (los) **conectar a través de puerta de enlace**.
   
   * Escriba un valor para **Nombre de conexión**. Por ejemplo, escriba `HISDEMO2`.
   * Escriba el valor de **nombre del servidor DB2**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `HISDEMO2.cloudapp.net:50000`.
   * Escriba un valor para **Nombre de la base de datos DB2**. Por ejemplo, escriba `NWIND`.
   * Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `db2admin`.
   * Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
9. Seleccione **crear** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
11. Si lo desea, seleccione **Mostrar opciones avanzadas** toospecify opciones de consulta.
12. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. Hola **Db2getRows** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
14. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir una lista de filas.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Agregar una fila mediante INSERT
Puede definir una lógica aplicación acción tooadd una fila en una tabla de DB2. Esta acción indica Hola conector tooprocess una instrucción INSERT de DB2, como `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `Db2insertRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **db2** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **DB2 - fila de inserción (vista previa)**.
6. Hola **DB2 - fila de inserción (vista previa)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuración, seleccione una conexión. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**, escriba `Area 99999` y escriba `102` para **REGIONID**. 
10. Seleccione **Guardar**.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. Hola **Db2insertRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
12. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la nueva fila de Hola.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Recuperar una fila mediante SELECT
Puede definir una lógica aplicación acción toofetch una fila en una tabla de DB2. Esta acción indica Hola conector tooprocess una instrucción SELECT WHERE para DB2, como `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre** (p. ej. "**Db2getRow**"), la **suscripción**, el **grupo de recursos**, la **ubicación** y el **plan de App Service**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista. 
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **db2** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **DB2 - Get filas (versión preliminar)**.
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuraciones, seleccione una conexión existente. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**. 
10. Si lo desea, seleccione **Mostrar opciones avanzadas** toospecify opciones de consulta.
11. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. Hola **Db2getRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
13. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la fila.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Cambiar una fila mediante UPDATE
Puede definir una lógica aplicación acción toochange una fila en una tabla de DB2. Esta acción indica Hola conector tooprocess una instrucción UPDATE de DB2, como `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `Db2updateRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **db2** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **DB2 - fila de la actualización (vista previa)**.
6. Hola **DB2 - fila de la actualización (vista previa)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuraciones, seleccione tooselect una conexión existente. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**, escriba `Updated 99999` y escriba `102` para **REGIONID**. 
10. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. Hola **Db2updateRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
12. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la nueva fila de Hola.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Quitar una fila mediante DELETE
Puede definir una lógica aplicación acción tooremove una fila en una tabla de DB2. Esta acción indica Hola conector tooprocess una instrucción DELETE de DB2, como `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `Db2deleteRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista. 
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, seleccione **db2** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **DB2 - Eliminar fila (versión preliminar)**.
6. Hola **DB2 - Eliminar fila (versión preliminar)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuraciones, seleccione una conexión existente. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**. 
10. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. Hola **Db2deleteRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
12. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la fila de hello eliminado.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Versiones y plataformas DB2 compatibles
Este conector es compatible con hello después plataformas IBM DB2 y las versiones, así como los productos compatibles de IBM DB2 (p. ej., IBM Bluemix dashDB) que admiten la arquitectura de base de datos relacionales (DRDA) distribuidas SQL Access Manager (SQLAM) versión 10 y 11:

* IBM DB2 para z/OS 11.1
* IBM DB2 para z/OS 10.1
* IBM DB2 para i 7.3
* IBM DB2 para i 7.2
* IBM DB2 para i 7.1
* IBM DB2 para LUW 11
* IBM DB2 para LUW 10.5

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/db2/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).

