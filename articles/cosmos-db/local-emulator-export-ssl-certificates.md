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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="e9e23-105">Exportar certificados de emulador de base de datos de Azure Cosmos Hola para su uso con Java, Python y Node.js</span><span class="sxs-lookup"><span data-stu-id="e9e23-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="e9e23-106">**Descargar Hola emulador**</span><span class="sxs-lookup"><span data-stu-id="e9e23-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="e9e23-107">Hello Azure Cosmos DB emulador proporciona un entorno local que emula Hola servicio de base de datos de Azure Cosmos para fines de desarrollo, incluido el uso de las conexiones SSL.</span><span class="sxs-lookup"><span data-stu-id="e9e23-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="e9e23-108">Esta entrada muestra cómo tooexport Hola SSL certificados para su uso en idiomas y tiempo de ejecución que no se integra con hello almacén de certificados de Windows, como Java que utiliza su propio [almacén de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) y Python que utiliza [socket contenedores](https://docs.python.org/2/library/ssl.html) y Node.js que utiliza [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="e9e23-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="e9e23-109">Puede leer más acerca del emulador de hello en [Hola de usar el emulador de base de datos de Azure Cosmos para desarrollo y pruebas](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="e9e23-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="e9e23-110">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e9e23-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e9e23-111">Rotación de certificados</span><span class="sxs-lookup"><span data-stu-id="e9e23-111">Rotating certificates</span></span>
> * <span data-ttu-id="e9e23-112">Exportación de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="e9e23-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="e9e23-113">Aprender cómo toouse Hola certificado en Java, Python y Node.js</span><span class="sxs-lookup"><span data-stu-id="e9e23-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="e9e23-114">Rotación de certificación</span><span class="sxs-lookup"><span data-stu-id="e9e23-114">Certification rotation</span></span>

<span data-ttu-id="e9e23-115">Certificados de hello que emulador Local de Azure Cosmos DB son generan Hola primera vez que se ejecuta el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e23-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="e9e23-116">Hay dos certificados.</span><span class="sxs-lookup"><span data-stu-id="e9e23-116">There are two certificates.</span></span> <span data-ttu-id="e9e23-117">Uno se utilizan para conectar un emulador local toohello y uno para la administración de secretos en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e23-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="e9e23-118">Hola certificado que desea tooexport es Hola conexión con el nombre descriptivo de Hola "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="e9e23-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="e9e23-119">Ambos certificados se pueden volver a generar, haga clic en **restablecer datos** tal y como se muestra a continuación del emulador de base de datos de Azure Cosmos ejecutándose en hello Bandeja de Windows.</span><span class="sxs-lookup"><span data-stu-id="e9e23-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="e9e23-120">Si volver a generar los certificados de Hola y tiene instalado en el almacén de certificados de Java de Hola o usado en otro lugar deberá tooupdate ellas, en caso contrario, la aplicación ya no pueda conectarse a un emulador local toohello.</span><span class="sxs-lookup"><span data-stu-id="e9e23-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Restablecimiento de datos en el emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="e9e23-122">¿Cómo tooexport Hola certificado SSL de base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="e9e23-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="e9e23-123">Inicie el Administrador de certificados de Windows hello ejecutando certlm.msc y vaya toohello Personal -> carpeta de certificados y el certificado de hello abierto con el nombre descriptivo de hello **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="e9e23-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Paso 1 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="e9e23-125">Haga clic en **Detalles** y, luego, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e9e23-125">Click on **Details** then **OK**.</span></span>

    ![Paso 2 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="e9e23-127">Haga clic en **copiar tooFile...** .</span><span class="sxs-lookup"><span data-stu-id="e9e23-127">Click **Copy tooFile...**.</span></span>

    ![Paso 3 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="e9e23-129">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e9e23-129">Click **Next**.</span></span>

    ![Paso 4 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="e9e23-131">Haga clic en **No exportar la clave privada** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e9e23-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Paso 5 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="e9e23-133">Haga clic en **X.509 codificado base 64 (. CER)** y luego en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e9e23-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Paso 6 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="e9e23-135">Asigne un nombre de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e23-135">Give hello certificate a name.</span></span> <span data-ttu-id="e9e23-136">En este caso, **documentdbemulatorcert** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e9e23-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Paso 7 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="e9e23-138">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="e9e23-138">Click **Finish**.</span></span>

    ![Paso 8 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="e9e23-140">¿Cómo toouse Hola certificado en Java</span><span class="sxs-lookup"><span data-stu-id="e9e23-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="e9e23-141">Al ejecutar las aplicaciones de Java o MongoDB que utilice el cliente de Java de Hola es más fácil tooinstall Hola certificado en almacén de certificados predeterminado de hello Java Hola pasar "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" marcas.</span><span class="sxs-lookup"><span data-stu-id="e9e23-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="e9e23-142">Por ejemplo Hola incluida [aplicación de demostración de Java](https://localhost:8081/_explorer/index.html) depende de almacén de certificados predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e23-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="e9e23-143">Siga las instrucciones de Hola Hola [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport Hola X.509 de certificado al almacén de certificados de Java de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e9e23-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="e9e23-144">Tenga en cuenta que trabajará en directorio de Hola % JAVA_HOME % cuando se ejecuta keytool.</span><span class="sxs-lookup"><span data-stu-id="e9e23-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="e9e23-145">Una vez Hola "CosmosDBEmulatorCertificate" SSL se instala el certificado de la aplicación debe ser capaz de tooconnect y use Hola emulador local de base de datos de Cosmos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e23-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="e9e23-146">Si sigues toohave problemas quizá le interese hello toofollow [depuración conexiones SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artículo.</span><span class="sxs-lookup"><span data-stu-id="e9e23-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="e9e23-147">Es muy probable que no está instalado el certificado de hello en el almacén de %JAVA_HOME%/jre/lib/security/cacerts Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e23-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="e9e23-148">Por ejemplo, si tiene varias versiones instaladas de la aplicación Java que esté utilizando un almacén cacerts diferentes de Hola uno que ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="e9e23-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="e9e23-149">¿Cómo toouse Hola certificado en Python</span><span class="sxs-lookup"><span data-stu-id="e9e23-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="e9e23-150">Por hello predeterminado [SDK(version 2.0.0 or higher) Python](documentdb-sdk-python.md) para hello API de documentos no intente y usar el certificado SSL de hello cuando se conecta un emulador local toohello.</span><span class="sxs-lookup"><span data-stu-id="e9e23-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="e9e23-151">Si pero desea toouse SSL validación puede seguir los ejemplos de hello en hello [contenedores de socket de Python](https://docs.python.org/2/library/ssl.html) documentación.</span><span class="sxs-lookup"><span data-stu-id="e9e23-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="e9e23-152">¿Cómo toouse Hola certificado en Node.js</span><span class="sxs-lookup"><span data-stu-id="e9e23-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="e9e23-153">Por hello predeterminado [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) para hello API de documentos no intente y usar el certificado SSL de hello cuando se conecta un emulador local toohello.</span><span class="sxs-lookup"><span data-stu-id="e9e23-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="e9e23-154">Si pero desea toouse SSL validación puede seguir los ejemplos de hello en hello [documentación de Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="e9e23-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9e23-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9e23-155">Next steps</span></span>

<span data-ttu-id="e9e23-156">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e9e23-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e9e23-157">Ha alternado certificados</span><span class="sxs-lookup"><span data-stu-id="e9e23-157">Rotated certificates</span></span>
> * <span data-ttu-id="e9e23-158">Certificado SSL de hello exportados</span><span class="sxs-lookup"><span data-stu-id="e9e23-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="e9e23-159">Aprender cómo toouse Hola certificado en Java, Python y Node.js</span><span class="sxs-lookup"><span data-stu-id="e9e23-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="e9e23-160">Ahora puede continuar toohello sección conceptos para obtener más información acerca de la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e9e23-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9e23-161">Distribución global</span><span class="sxs-lookup"><span data-stu-id="e9e23-161">Global distribution</span></span>](distribute-data-globally.md) 
