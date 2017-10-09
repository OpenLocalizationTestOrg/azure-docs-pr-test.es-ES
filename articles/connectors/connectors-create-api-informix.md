---
title: "Conector de Informix aaaAdd hello en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general del conector de Informix con parámetros de la API de REST"
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Empezar a trabajar con el conector de Informix Hola
Conector de Microsoft para Informix conecta tooresources Logic Apps almacenados en una base de datos de IBM Informix. Conector de Informix Hola incluye un Microsoft toocommunicate tooremote Informix servidor los equipos cliente a través de una red TCP/IP. Esto incluye las bases de datos en la nube, como IBM Informix para Windows que se ejecuta en la virtualización de Azure y un bases de datos mediante la puerta de enlace de datos de Hola de local a local. Vea hello [admite lista](connectors-create-api-informix.md#supported-informix-platforms-and-versions) de plataformas de IBM Informix y las versiones (en este tema).

Conector de Hello admite hello las siguientes operaciones de base de datos:

* Mostrar tablas de base de datos
* Leer una fila mediante SELECT
* Leer todas las filas mediante SELECT
* Agregar una fila mediante INSERT
* Modificar una fila mediante UPDATE
* Quitar una fila mediante DELETE

Este tema muestra cómo toouse conector de hello en un tooprocess de aplicación lógica la base de las operaciones de datos.

toolearn más información acerca de las aplicaciones lógicas, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Acciones disponibles
Este conector es compatible con hello siguientes acciones de aplicación lógica:

* Getables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Enumeración de tablas
Crear una aplicación de la lógica para cualquier operación consta de varios pasos que se realiza a través del portal de Microsoft Azure Hola.

Dentro de la aplicación de la lógica de hello, puede agregar las tablas de toolist de acción en una base de datos de Informix. Esta acción indica Hola conector tooprocess una instrucción de esquema Informix, como `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `InformixgetTables`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**.  
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **informix** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **Informix - Get tablas (versión preliminar)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. Hola **Informix - Get tablas** panel de configuración, seleccione **casilla** tooenable **conectar a través de puerta de enlace de datos local**. Observe que cambia configuración de Hola de nube local tooon.
   
   * Escriba el valor de **Server**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `ibmserver01:9089`.
   * Escriba un valor para **Base de datos**. Por ejemplo, escriba `nwind`.
   * Seleccione un valor para **Autenticación**. Por ejemplo, seleccione **Básico**.
   * Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `informix`.
   * Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
   * Seleccione el valor para **Puerta de enlace**. Por ejemplo, seleccione **datagateway01**.
7. Seleccione **Crear** y, a continuación, seleccione **Guardar**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. Hola **InformixgetTables** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
9. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_tables**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir una lista de tablas.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Crear conexiones de Hola
Este conector es compatible con las conexiones toodatabase local y en la nube de hello utilizando Hola siguientes propiedades de conexión. 

| Propiedad | Description |
| --- | --- |
| Servidor |Obligatorio. Acepta un valor de cadena que representa una dirección TCP/IP o alias en formato IPv4 o IPv6 seguido de un número de puerto TCP/IP (delimitado por dos puntos). |
| Base de datos |Obligatorio. Acepta un valor de cadena que representa un nombre de base de datos relacional de DRDA (RDBNAM). Informix acepta una cadena de 128 bytes (la base de datos se conoce como una base de datos IBM Informix (dbname)). |
| Autenticación |Opcional. Acepta un valor de elemento de lista que puede ser Basic o Windows (kerberos). |
| Nombre de usuario |Obligatorio. Acepta un valor de cadena. |
| Contraseña |Obligatorio. Acepta un valor de cadena. |
| Puerta de enlace |Necesario. Acepta un valor de elemento de lista, que representa Hola local datos definido de la puerta de enlace tooLogic aplicaciones en el grupo de almacenamiento de Hola. |

## <a name="create-hello-on-premises-gateway-connection"></a>Crear conexiones de puerta de enlace de hello local
Este conector puede tener acceso a una base de datos de Informix local mediante la puerta de enlace de datos de hello en local. Consulte los temas sobre puertas de enlace para más información. 

1. Hola **puertas de enlace** panel de configuración, seleccione **casilla** tooenable **conectar a través de puerta de enlace**. Vea Hola cambia configuración de nube local tooon.
2. Escriba el valor de **Server**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `ibmserver01:9089`.
3. Escriba un valor para **Base de datos**. Por ejemplo, escriba `nwind`.
4. Seleccione un valor para **Autenticación**. Por ejemplo, seleccione **Básico**.
5. Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `informix`.
6. Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
7. Seleccione el valor para **Puerta de enlace**. Por ejemplo, seleccione **datagateway01**.
8. Seleccione **crear** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Crear la conexión de hello en la nube
Este conector puede tener acceso a una base de datos Informix en la nube. 

1. Hola **puertas de enlace** panel de configuración, deje hello **casilla** deshabilitado (los) **conectar a través de puerta de enlace**. 
2. Escriba un valor para **Nombre de conexión**. Por ejemplo, escriba `hisdemo2`.
3. Escriba el valor de **nombre del servidor Informix**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `hisdemo2.cloudapp.net:9089`.
4. Escriba un valor para **Nombre de la base de datos Informix**. Por ejemplo, escriba `nwind`.
5. Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `informix`.
6. Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
7. Seleccione **crear** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Recuperar todas las filas mediante SELECT
Puede crear un toofetch de acción de aplicación lógica todas las filas de tabla de Informix Hola. Esta acción indica Hola conector tooprocess una instrucción SELECT de Informix, como `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre** (p. ej. "**InformixgetRows**"), la **suscripción**, el **grupo de recursos**, la **ubicación** y el **plan de App Service**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **informix** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **Informix - Get filas (versión preliminar)** .
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**.
7. Hola **conexiones** panel de configuración, seleccione **crear nuevo**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. Hola **puertas de enlace** panel de configuración, deje hello **casilla** deshabilitado (los) **conectar a través de puerta de enlace**.
   
   * Escriba un valor para **Nombre de conexión**. Por ejemplo, escriba `HISDEMO2`.
   * Escriba el valor de **nombre del servidor Informix**, en forma de Hola de dirección o alias de número de puerto de dos puntos. Por ejemplo, escriba `HISDEMO2.cloudapp.net:9089`.
   * Escriba un valor para **Nombre de la base de datos Informix**. Por ejemplo, escriba `NWIND`.
   * Escriba un valor para **Nombre de usuario**. Por ejemplo, escriba `informix`.
   * Escriba un valor para **Contraseña**. Por ejemplo, escriba `Password1`.
9. Seleccione **crear** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
11. Si lo desea, seleccione **Mostrar opciones avanzadas** toospecify opciones de consulta.
12. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. Hola **InformixgetRows** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
14. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir una lista de filas.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Agregar una fila mediante INSERT
Puede crear una lógica aplicación acción tooadd una fila en una tabla de Informix. Esta acción indica Hola conector tooprocess una instrucción INSERT de Informix, como `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `InformixinsertRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **informix** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **Informix - fila de inserción (vista previa)**.
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuración, seleccione tooselect una conexión. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**, escriba `Area 99999` y escriba `102` para **REGIONID**. 
10. Seleccione **Guardar**.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. Hola **InformixinsertRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
12. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la nueva fila de Hola.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Recuperar una fila mediante SELECT
Puede crear una lógica aplicación acción toofetch una fila en una tabla de Informix. Esta acción indica Hola conector tooprocess una instrucción SELECT WHERE para Informix, como `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `InformixgetRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **informix** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **Informix - Get filas (versión preliminar)** .
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuraciones, seleccione tooselect una conexión existente. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**. 
10. Si lo desea, seleccione **Mostrar opciones avanzadas** toospecify opciones de consulta.
11. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. Hola **InformixgetRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
13. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la fila.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Cambiar una fila mediante UPDATE
Puede crear una lógica aplicación acción toochange una fila en una tabla de Informix. Esta acción indica Hola conector tooprocess una instrucción UPDATE de Informix, como `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `InformixupdateRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **informix** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **Informix - fila de la actualización (vista previa)**.
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuraciones, seleccione tooselect una conexión existente. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**, escriba `Updated 99999` y escriba `102` para **REGIONID**. 
10. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. Hola **InformixupdateRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
12. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la nueva fila de Hola.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Quitar una fila mediante DELETE
Puede crear una lógica aplicación acción tooremove una fila en una tabla de Informix. Esta acción indica Hola conector tooprocess una instrucción DELETE Informix, como `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica
1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.
2. Escriba hello **nombre**, como `InformixdeleteRow`, **suscripción**, **grupo de recursos**, **ubicación**, y **aplicación Plan de servicio**. Seleccione **Pin toodashboard**y, a continuación, seleccione **crear**.

### <a name="add-a-trigger-and-action"></a>Agregar un desencadenador y acción
1. Hola **el Diseñador de aplicaciones de la lógica de**, seleccione **LogicApp en blanco** en hello **plantillas** lista.
2. Hola **desencadenadores** lista, seleccione **periodicidad**. 
3. Hola **periodicidad** desencadenador, seleccione **editar**, seleccione **frecuencia** desplegable tooselect **día**y, a continuación, seleccione  **Intervalo de** tootype **7**. 
4. Seleccione hello **+ nuevo paso** cuadro y, a continuación, seleccione **agregar una acción**.
5. Hola **acciones** lista, escriba **informix** en hello **buscar más acciones** cuadro de edición y, a continuación, seleccione **Informix - Eliminar fila (versión preliminar)**.
6. Hola **obtener filas (versión preliminar)** acción, seleccione **cambiar conexión**. 
7. Hola **conexiones** panel de configuraciones, seleccione una conexión existente. Por ejemplo, seleccione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hola **nombre de la tabla** lista, seleccione hello **flecha abajo**y, a continuación, seleccione **área**.
9. Escriba valores para todas las columnas obligatorias (busque un asterisco rojo). Por ejemplo, escriba `99999` para **AREAID**. 
10. Seleccione **Guardar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. Hola **InformixdeleteRow** hoja, dentro de hello **todas las ejecuciones de** lista en **resumen**, seleccione Hola indicado por el primer elemento (última ejecución).
12. Hola **aplicación lógica ejecutar** hoja, seleccione **detalles de la ejecución**. Dentro de hello **acción** lista, seleccione **Get_rows**. Ver Hola valor **estado**, que debe ser **correcto**. Seleccione hello **vínculo entradas** entradas de hello tooview. Seleccione hello **salidas vínculo**y genera Hola vista; que debe incluir la fila de hello eliminado.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Versiones y plataformas Informix compatibles
Este conector es compatible con hello las siguientes versiones de IBM Informix, cuando configura las conexiones de cliente de arquitectura de base de datos relacionales (DRDA) distribuidas toosupport.

* IBM Informix 12.1
* IBM Informix 11.7

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/informix/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).

