---
title: certificados de emulador de base de datos de Azure Cosmos hello aaaExport | Documentos de Microsoft
description: "Al desarrollar en idiomas y tiempos de ejecución que no utilizan el almacén de certificados de Windows hello necesitará tooexport y administrar los certificados SSL de Hola. Esta publicación proporciona instrucciones detalladas para ello."
services: cosmos-db
documentationcenter: 
keywords: Emulador de Azure Cosmos DB
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Exportar certificados de emulador de base de datos de Azure Cosmos Hola para su uso con Java, Python y Node.js

[**Descargar Hola emulador**](https://aka.ms/cosmosdb-emulator)

Hello Azure Cosmos DB emulador proporciona un entorno local que emula Hola servicio de base de datos de Azure Cosmos para fines de desarrollo, incluido el uso de las conexiones SSL. Esta entrada muestra cómo tooexport Hola SSL certificados para su uso en idiomas y tiempo de ejecución que no se integra con hello almacén de certificados de Windows, como Java que utiliza su propio [almacén de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) y Python que utiliza [socket contenedores](https://docs.python.org/2/library/ssl.html) y Node.js que utiliza [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Puede leer más acerca del emulador de hello en [Hola de usar el emulador de base de datos de Azure Cosmos para desarrollo y pruebas](./local-emulator.md).

Este tutorial trata Hola siguientes tareas:

> [!div class="checklist"]
> * Rotación de certificados
> * Exportación de certificados SSL
> * Aprender cómo toouse Hola certificado en Java, Python y Node.js

## <a name="certification-rotation"></a>Rotación de certificación

Certificados de hello que emulador Local de Azure Cosmos DB son generan Hola primera vez que se ejecuta el emulador de Hola. Hay dos certificados. Uno se utilizan para conectar un emulador local toohello y uno para la administración de secretos en el emulador de Hola. Hola certificado que desea tooexport es Hola conexión con el nombre descriptivo de Hola "DocumentDBEmulatorCertificate".

Ambos certificados se pueden volver a generar, haga clic en **restablecer datos** tal y como se muestra a continuación del emulador de base de datos de Azure Cosmos ejecutándose en hello Bandeja de Windows. Si volver a generar los certificados de Hola y tiene instalado en el almacén de certificados de Java de Hola o usado en otro lugar deberá tooupdate ellas, en caso contrario, la aplicación ya no pueda conectarse a un emulador local toohello.

![Restablecimiento de datos en el emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>¿Cómo tooexport Hola certificado SSL de base de datos de Azure Cosmos

1. Inicie el Administrador de certificados de Windows hello ejecutando certlm.msc y vaya toohello Personal -> carpeta de certificados y el certificado de hello abierto con el nombre descriptivo de hello **DocumentDbEmulatorCertificate**.

    ![Paso 1 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Haga clic en **Detalles** y, luego, en **Aceptar**.

    ![Paso 2 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Haga clic en **copiar tooFile...** .

    ![Paso 3 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Haga clic en **Siguiente**.

    ![Paso 4 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Haga clic en **No exportar la clave privada** y, luego, haga clic en **Siguiente**.

    ![Paso 5 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Haga clic en **X.509 codificado base 64 (. CER)** y luego en **Siguiente**.

    ![Paso 6 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Asigne un nombre de certificado de Hola. En este caso, **documentdbemulatorcert** y, luego, haga clic en **Siguiente**.

    ![Paso 7 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Haga clic en **Finalizar**

    ![Paso 8 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>¿Cómo toouse Hola certificado en Java

Al ejecutar las aplicaciones de Java o MongoDB que utilice el cliente de Java de Hola es más fácil tooinstall Hola certificado en almacén de certificados predeterminado de hello Java Hola pasar "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" marcas. Por ejemplo Hola incluida [aplicación de demostración de Java](https://localhost:8081/_explorer/index.html) depende de almacén de certificados predeterminado de Hola.

Siga las instrucciones de Hola Hola [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport Hola X.509 de certificado al almacén de certificados de Java de Hola de forma predeterminada. Tenga en cuenta que trabajará en directorio de Hola % JAVA_HOME % cuando se ejecuta keytool.

Una vez Hola "CosmosDBEmulatorCertificate" SSL se instala el certificado de la aplicación debe ser capaz de tooconnect y use Hola emulador local de base de datos de Cosmos de Azure. Si sigues toohave problemas quizá le interese hello toofollow [depuración conexiones SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artículo. Es muy probable que no está instalado el certificado de hello en el almacén de %JAVA_HOME%/jre/lib/security/cacerts Hola. Por ejemplo, si tiene varias versiones instaladas de la aplicación Java que esté utilizando un almacén cacerts diferentes de Hola uno que ha actualizado.

## <a name="how-toouse-hello-certificate-in-python"></a>¿Cómo toouse Hola certificado en Python

Por hello predeterminado [SDK(version 2.0.0 or higher) Python](documentdb-sdk-python.md) para hello API de documentos no intente y usar el certificado SSL de hello cuando se conecta un emulador local toohello. Si pero desea toouse SSL validación puede seguir los ejemplos de hello en hello [contenedores de socket de Python](https://docs.python.org/2/library/ssl.html) documentación.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>¿Cómo toouse Hola certificado en Node.js

Por hello predeterminado [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) para hello API de documentos no intente y usar el certificado SSL de hello cuando se conecta un emulador local toohello. Si pero desea toouse SSL validación puede seguir los ejemplos de hello en hello [documentación de Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Ha alternado certificados
> * Certificado SSL de hello exportados
> * Aprender cómo toouse Hola certificado en Java, Python y Node.js

Ahora puede continuar toohello sección conceptos para obtener más información acerca de la base de datos de Cosmos.

> [!div class="nextstepaction"]
> [Distribución global](distribute-data-globally.md) 
