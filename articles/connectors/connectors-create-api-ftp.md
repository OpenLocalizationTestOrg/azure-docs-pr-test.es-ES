---
title: "aaaLearn cómo toouse Hola conector FTP en las aplicaciones lógicas | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conectar tooFTP server toomanage los archivos. En FTP, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Empezar a trabajar con el conector FTP de Hola
Usar Hola FTP conector toomonitor, administrar y crear archivos en un servidor FTP. 

toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica. Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Conectar tooFTP
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio. Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.  

### <a name="create-a-connection-tooftp"></a>Crear una conexión tooFTP
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Uso de un desencadenador de FTP
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> conector FTP de Hello requiere un servidor FTP que es accesible desde Internet hello y está configurada toooperate con el modo pasivo. Además, el conector de hello FTP es **no es compatible con implícita FTPS (FTP sobre SSL)**. conector FTP de Hello solo admite explícita FTPS (FTP sobre SSL).  
> 
> 

En este ejemplo, le mostrará cómo hello toouse **FTP: cuando se agrega o modifica un archivo** desencadenar tooinitiate un flujo de trabajo de aplicación lógica cuando se agregan a un archivo, o modifica en un servidor FTP. En un ejemplo de la empresa, podría utilizar este toomonitor desencadenador una carpeta FTP para los archivos nuevos que representan los pedidos de los clientes.  A continuación, podría utilizar una acción de conector FTP como **obtener el contenido del archivo** tooget contenido de Hola Hola del orden de para su posterior procesamiento y almacenamiento en la base de datos de pedidos.

1. Escriba *ftp* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de lógica de hello, a continuación, seleccione hello **FTP: cuando se agrega o modifica un archivo** desencadenador   
   ![Imagen de desencadenador de FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Hola **cuando se agrega o modifica un archivo** abrirá control  
   ![Imagen de desencadenador de FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Seleccione hello **...**  ubicado en hello derecha del control de Hola. Esto abre el control de selector de carpeta Hola  
   ![Imagen de desencadenador de FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Seleccione hello  **>**  (flecha derecha) y busque la carpeta de hello toofind que desea toomonitor para archivos nuevos o modificados. Seleccione la carpeta de hello y observe carpeta Hola aparece ahora en hello **carpeta** control.  
   ![Imagen de desencadenador de FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

En este punto, la aplicación lógica se ha configurado con un desencadenador que comience una ejecución del programa Hola a otros desencadenadores y acciones de flujo de trabajo de hello cuando un archivo se modifica o se crea en carpeta FTP específico de Hola. 

> [!NOTE]
> Para que una toobe de aplicación lógica funcional, debe contener al menos un desencadenador y una acción. Siga los pasos de Hola Hola siguiente sección tooadd una acción.  
> 
> 

## <a name="use-a-ftp-action"></a>Uso de una acción de FTP
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Ahora que ha agregado un desencadenador, siga estas tooadd pasos una acción que van a obtener contenido de Hola de hello nuevos o modificados se encuentra el archivo desencadenador Hola.    

1. Seleccione **+ nuevo paso** tooadd Hola Hola acción tooget Hola contenido de archivo hello en servidor hello FTP  
2. Seleccione hello **agregar una acción** vínculo.  
   ![Imagen de acción de FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Escriba *FTP* toosearch para todas las acciones relacionadas con tooFTP.
4. Seleccione **FTP: obtener el contenido del archivo** como Hola tootake acción cuando un archivo nuevo o modificado se encuentra en la carpeta de hello FTP.      
   ![Imagen de acción de FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Hola **obtener el contenido del archivo** controlar se abre. **Tenga en cuenta**: será solicitada tooauthorize su tooaccess de aplicación lógica, el servidor FTP de la cuenta si aún no lo hecho previamente.  
   ![Imagen de acción de FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Seleccione hello **archivo** control (Hola espacios en blanco que se encuentra debajo de **archivo***). En este caso, puede utilizar cualquiera de hello varias propiedades de hello nuevos o modificados se encuentra el archivo en el servidor FTP de Hola.  
6. Seleccione hello **el contenido del archivo** opción.  
   ![Imagen de acción de FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. se actualiza el control Hello, que indica que hello **FTP: obtener el contenido del archivo** acción obtendrá hello *el contenido del archivo* del archivo de Hola nuevos o modificados en el servidor de hello FTP.      
   ![Imagen de acción de FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Guarde su trabajo, a continuación, agregue un tootest de carpeta de archivo toohello FTP en el flujo de trabajo.    

En este momento, ha sido la aplicación de la lógica de hello configurado con un desencadenador toomonitor una carpeta en un servidor FTP y el flujo de trabajo de hello iniciar cuando encuentra un nuevo archivo o abrir un archivo modificado en el servidor de hello FTP. 

aplicación de la lógica de Hello también se ha configurado con un contenido de Hola de acción tooget del archivo Hola de nuevo o modificado.

Ahora puede agregar otra acción, como hello [SQL Server - Insertar fila](connectors-create-api-sqlazure.md) contenido de hello tooinsert de acción del archivo de hello nuevos o modificados en una tabla de base de datos SQL.  

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md)

