---
title: "Conector de base de datos de Oracle aaaAdd hello en sus aplicaciones de la lógica de Azure | Documentos de Microsoft"
description: "Usar el conector de base de datos de Oracle de hello en una aplicación de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Empezar a trabajar con el conector de base de datos de Oracle Hola

Mediante el conector de base de datos de Oracle de hello, crear organizativas flujos de trabajo que utilizan datos de la base de datos existente. Este conector puede conectarse tooan base de datos de Oracle local o una máquina virtual de Azure con la base de datos de Oracle instalada. Con este conector, puede hacer lo siguiente:

* Compilar el flujo de trabajo mediante la adición de una base de datos de los clientes de tooa cliente nuevo o actualizar un pedido en una base de datos de pedidos.
* Usar acciones tooget una fila de datos, insertar una fila nueva e incluso eliminar. Por ejemplo, al crear un registro en Dynamics CRM Online (un desencadenador), inserte una fila en una base de datos de Oracle (una acción). 

Este tema muestra cómo toouse Hola conector de base de datos de Oracle en una aplicación de lógica.

## <a name="prerequisites"></a>Requisitos previos

* Versiones de Oracle compatibles: 
    * Oracle 9 y versiones posteriores
    * Software cliente de Oracle 8.1.7 y posteriores

* Hola de instalación local de puerta de enlace de datos. [Conectar datos tooon locales desde las aplicaciones lógicas](../logic-apps/logic-apps-gateway-connection.md) listas Hola pasos. puerta de enlace de Hello es necesario tooconnect tooan base de datos de Oracle local o una máquina virtual de Azure con la base de datos de Oracle instalada. 

    > [!NOTE]
    > puerta de enlace de datos de Hello local actúa como un puente y proporciona a una transferencia de datos seguros entre los datos locales (datos que no están en la nube de hello) y las aplicaciones lógicas. Hola misma puerta de enlace se puede utilizar con varios servicios y varios orígenes de datos. Por lo tanto, puede que solo tenga puerta de enlace de hello tooinstall una vez.

* Instalar Hola cliente de Oracle en la máquina de Hola donde instaló la puerta de enlace de datos de hello en local. Asegúrese de tooinstall Hola proveedor de datos de Oracle de 64 bits para .NET de Oracle:  

  [64-bits ODAC 12c versión 4 (12.1.0.2.4) para Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Si no está instalado el cliente de Oracle de hello, se produce un error cuando intente toocreate o usar conexión de Hola. Consulte los errores comunes de hello en este tema.


## <a name="add-hello-connector"></a>Agregar conector Hola

> [!IMPORTANT]
> Este conector no tiene ningún desencadenador. Solo tiene acciones. Por lo que cuando se crea la aplicación lógica, agregue otro toostart de desencadenador la aplicación lógica, como **programación - periodicidad**, o **de solicitud / respuesta - respuesta**. 

1. Hola [portal de Azure](https://portal.azure.com), cree una aplicación lógica en blanco.

2. En el inicio de saludo de la aplicación lógica, seleccione hello **de solicitud / respuesta - solicitud** desencadenador: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Seleccione **Guardar**. Cuando lo guarde, se generará automáticamente la URL de solicitud. 

4. Seleccione **Nuevo paso** y seleccione **Agregar una acción**. Escriba `oracle` toosee Hola acciones disponibles: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Esto también es toosee de manera más rápida de Hola Hola desencadenadores y las acciones disponibles para cualquier conector. Tipo de parte del nombre de conector de hello, como `oracle`. Diseñador de Hello enumera todos los desencadenadores y las medidas. 

5. Seleccione una de las acciones de hello, como **base de datos de Oracle - Get fila**. Seleccione **Connect via on-premises data gateway** (Conectarse a través de la puerta de enlace de datos local). Escriba el nombre de servidor de Oracle de hello, método de autenticación, nombre de usuario, contraseña y puerta de enlace de hello seleccione:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Una vez conectado, seleccione una tabla en la lista de Hola y especifique la tabla de tooyour de Id. de fila de Hola. Necesita tabla toohello de tooknow Hola identificador. Si no sabe, póngase en contacto con el Administrador de base de datos de Oracle y obtener un resultado de hello `select * from yourTableName`. Esto deja Hola necesita tooproceed de información de identificación.

    En el siguiente ejemplo de Hola, datos del trabajo que se devuelve desde una base de datos de recursos humanos: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. En este paso siguiente, puede usar cualquiera de hello otro toobuild conectores el flujo de trabajo. Si desea obtener los datos de Oracle tootest, envíe un correo electrónico con datos de Oracle de hello mediante uno de hello enviar conectores de correo electrónico, Office 365 o Gmail. Usar tokens dinámica de Hola de Hola Hola de toobuild de tabla de Oracle `Subject` y `Body` de tu correo electrónico:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Guarde** la aplicación lógica y, a continuación, seleccione **Ejecutar**. Cierre el Diseñador de Hola y examine Hola historial de ejecuciones para el estado de Hola. Si se produce un error, seleccione la fila de mensajes con errores de Hola. Hola diseñador se abre y muestra qué paso no se pudo y también muestra información de error de Hola. Si se realiza correctamente, debería recibir un correo electrónico con información de Hola que agregó.


### <a name="workflow-ideas"></a>Ideas de flujo de trabajo

* Que desee toomonitor hello #oracle hashtag y coloca tweets hello en una base de datos, por lo que se pueden consultar y usar en otras aplicaciones. En una aplicación de lógica, agregue hello `Twitter - When a new tweet is posted` desencadenar y escriba hello **#oracle** hashtag. A continuación, agregue hello `Oracle Database - Insert row` acción y seleccione la tabla:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* Cola de Bus de servicio tooa se envían los mensajes. Desea tooget estos mensajes y colóquelos en una base de datos. En una aplicación de lógica, agregue hello `Service Bus - when a message is received in a queue` desencadenador y seleccione Hola cola. A continuación, agregue hello `Oracle Database - Insert row` acción y seleccione la tabla:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Errores comunes

#### <a name="error-cannot-reach-hello-gateway"></a>**Error**: no se puede alcanzar Hola puerta de enlace

**Causa**: puerta de enlace de datos de hello local no es capaz de tooconnect toohello en la nube. 

**Mitigación**: asegúrese de que la puerta de enlace está ejecutando en la máquina de hello local donde se instaló y que TI puede conectarse toohello internet.  Se recomienda no instalar la puerta de enlace de hello en un equipo que puede desactivarse o suspensión. También puede reiniciar el servicio de puerta de enlace de datos de hello local (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Error**: proveedor de Hola que se utiliza está en desuso: ' System.Data.OracleClient requiere la versión 8.1.7 del software cliente de Oracle o superior.'. Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) proveedor oficial de tooinstall Hola.

**Causa**: puerta de enlace de datos se ejecuta en instalaciones de cliente de Oracle Hola SDK no está instalado en el equipo de Hola donde hello.  

**Resolución**: descargar e instalar el SDK de cliente de Oracle de hello en hello mismo equipo como puerta de enlace de datos de hello en local.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Error**: La tabla '[Tablename]' no define las columnas clave.

**Causa**: Hola tabla no tiene ninguna clave principal.  

**Resolución**: conector de base de datos de Oracle Hola requiere que se utilice una tabla con una columna de clave principal.

#### <a name="currently-not-supported"></a>Actualmente no se admite

* Vistas y procedimientos almacenados 
* Todas las tablas con claves compuestas
* Tipos de objetos anidados en tablas
 
## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/oracle/). 

## <a name="get-some-help"></a>Obtener ayuda

Hola [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) es una gran colocar tooask preguntas, responda a preguntas y ver lo que hacen otros usuarios de las aplicaciones lógicas. 

Puede ayudar a mejorar Logic Apps y conectores al votar y enviar sus ideas en [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Pasos siguientes
[Crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md)y explorar los conectores disponibles de hello en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).
