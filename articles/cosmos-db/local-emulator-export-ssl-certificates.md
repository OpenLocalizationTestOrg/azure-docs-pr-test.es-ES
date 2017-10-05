---
title: "Exportación de los certificados del emulador de Azure Cosmos DB | Microsoft Docs"
description: "Al desarrollar en lenguajes y tiempos de ejecución que no utilizan el almacén de certificados de Windows, debe exportar y administrar los certificados SSL. Esta publicación proporciona instrucciones detalladas para ello."
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
ms.openlocfilehash: 4add5028d50972316902cecd8c399781c012cb77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="3ccdb-105">Exportación de los certificados del emulador de Azure Cosmos DB para su uso con Java, Python y Node.js</span><span class="sxs-lookup"><span data-stu-id="3ccdb-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="3ccdb-106">**Descarga del Emulador**</span><span class="sxs-lookup"><span data-stu-id="3ccdb-106">**Download the Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="3ccdb-107">El emulador de Azure Cosmos DB proporciona un entorno local que emula el servicio Azure Cosmos DB con fines de desarrollo, incluido su uso de las conexiones SSL.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="3ccdb-108">En esta publicación se muestra cómo exportar los certificados SSL para su uso en lenguajes y entornos de ejecución que no se integran con el almacén de certificados de Windows, como Java, que utiliza su propio [almacén de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), Python, que usa [contenedores de sockets](https://docs.python.org/2/library/ssl.html) y Node.js, que usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="3ccdb-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="3ccdb-109">Puede leer más sobre el emulador en el artículo [Uso del emulador de Azure Cosmos DB para desarrollo y pruebas](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3ccdb-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="3ccdb-110">En este tutorial se describen las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ccdb-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ccdb-111">Rotación de certificados</span><span class="sxs-lookup"><span data-stu-id="3ccdb-111">Rotating certificates</span></span>
> * <span data-ttu-id="3ccdb-112">Exportación de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="3ccdb-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="3ccdb-113">Obtener información sobre cómo usar el certificado en Java, Python y Node.js</span><span class="sxs-lookup"><span data-stu-id="3ccdb-113">Learning how to use the certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="3ccdb-114">Rotación de certificación</span><span class="sxs-lookup"><span data-stu-id="3ccdb-114">Certification rotation</span></span>

<span data-ttu-id="3ccdb-115">Los certificados del emulador local de Azure Cosmos DB se generan la primera vez que se ejecuta el emulador.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span></span> <span data-ttu-id="3ccdb-116">Hay dos certificados.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-116">There are two certificates.</span></span> <span data-ttu-id="3ccdb-117">Uno se utiliza para la conexión con el emulador local y otro para la administración de secretos en el emulador.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span></span> <span data-ttu-id="3ccdb-118">El certificado que desea exportar es el certificado de conexión con el nombre descriptivo "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="3ccdb-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="3ccdb-119">Ambos certificados se pueden regenerar; para ello, haga clic en **Restablecer datos** tal y como se muestra a continuación desde el emulador de Azure Cosmos DB que se ejecuta en la Bandeja de Windows.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span></span> <span data-ttu-id="3ccdb-120">Si regenera los certificados y los tiene instalados en el almacén de certificados de Java o los usa en otro lugar, deberá actualizarlos; en caso contrario, la aplicación ya no se conectará al emulador local.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span></span>

![Restablecimiento de datos en el emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="3ccdb-122">Exportación del certificado SSL de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3ccdb-122">How to export the Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="3ccdb-123">Inicie el administrador de certificados de Windows; para ello, ejecute certlm.msc, vaya a la carpeta Personal-> Certificados y abra el certificado con el nombre descriptivo **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Paso 1 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="3ccdb-125">Haga clic en **Detalles** y, luego, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-125">Click on **Details** then **OK**.</span></span>

    ![Paso 2 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="3ccdb-127">Haga clic en **Copiar en archivo...** .</span><span class="sxs-lookup"><span data-stu-id="3ccdb-127">Click **Copy to File...**.</span></span>

    ![Paso 3 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="3ccdb-129">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-129">Click **Next**.</span></span>

    ![Paso 4 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="3ccdb-131">Haga clic en **No exportar la clave privada** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Paso 5 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="3ccdb-133">Haga clic en **X.509 codificado base 64 (. CER)** y luego en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Paso 6 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="3ccdb-135">Asigne un nombre al certificado.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-135">Give the certificate a name.</span></span> <span data-ttu-id="3ccdb-136">En este caso, **documentdbemulatorcert** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Paso 7 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="3ccdb-138">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="3ccdb-138">Click **Finish**.</span></span>

    ![Paso 8 de exportación de un emulador local de Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a><span data-ttu-id="3ccdb-140">Uso del certificado en Java</span><span class="sxs-lookup"><span data-stu-id="3ccdb-140">How to use the certificate in Java</span></span>

<span data-ttu-id="3ccdb-141">Al ejecutar aplicaciones de Java o MongoDB que utilizan el cliente de Java, es más fácil instalar el certificado en el almacén de certificados predeterminado de Java que pasar las marcas "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="3ccdb-142">Por ejemplo, la [aplicación de demostración de Java](https://localhost:8081/_explorer/index.html) incluida depende del almacén de certificados predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span></span>

<span data-ttu-id="3ccdb-143">Siga las instrucciones de la publicación [Incorporación de un certificado al almacén de certificados CA de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) para importar el certificado X.509 en el almacén de certificados de Java.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span></span> <span data-ttu-id="3ccdb-144">Tenga en cuenta que trabajará en el directorio %JAVA_HOME% al ejecutar keytool.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="3ccdb-145">Una vez que el certificado SSL "CosmosDBEmulatorCertificate" está instalado en la aplicación, debe poder conectarse y utilizar el emulador de Azure Cosmos DB local.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="3ccdb-146">Si sigue teniendo problemas, puede seguir los pasos indicados en el artículo [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) (Depuración de conexiones SSL/TLS).</span><span class="sxs-lookup"><span data-stu-id="3ccdb-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="3ccdb-147">Es muy probable que el certificado no esté instalado en el almacén %JAVA_HOME%/jre/lib/security/cacerts.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="3ccdb-148">Por ejemplo, si tiene varias versiones instaladas de Java, es probable que la aplicación esté utilizando un almacén de certificados CA diferente del actualizado.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span></span>

## <a name="how-to-use-the-certificate-in-python"></a><span data-ttu-id="3ccdb-149">Uso del certificado en Python</span><span class="sxs-lookup"><span data-stu-id="3ccdb-149">How to use the certificate in Python</span></span>

<span data-ttu-id="3ccdb-150">De forma predeterminada, el [SDK de Python (versión 2.0.0 o posterior)](documentdb-sdk-python.md) para la API de DocumentDB no probará ni usará el certificado SSL al conectarse con el emulador local.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-150">By default the [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="3ccdb-151">Sin embargo, si desea utilizar la validación de SSL, puede seguir los ejemplos de la documentación de los [contenedores de sockets de Python](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="3ccdb-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-to-use-the-certificate-in-nodejs"></a><span data-ttu-id="3ccdb-152">Uso del certificado en Node.js</span><span class="sxs-lookup"><span data-stu-id="3ccdb-152">How to use the certificate in Node.js</span></span>

<span data-ttu-id="3ccdb-153">De forma predeterminada, el [SDK de Node.js (versión 1.10.1 o posterior)](documentdb-sdk-node.md) para la API de DocumentDB no probará ni usará el certificado SSL al conectarse con el emulador local.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-153">By default the [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="3ccdb-154">Sin embargo, si desea utilizar la validación de SSL, puede seguir los ejemplos de la [documentación de Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="3ccdb-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ccdb-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ccdb-155">Next steps</span></span>

<span data-ttu-id="3ccdb-156">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ccdb-156">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ccdb-157">Ha alternado certificados</span><span class="sxs-lookup"><span data-stu-id="3ccdb-157">Rotated certificates</span></span>
> * <span data-ttu-id="3ccdb-158">Ha exportado el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="3ccdb-158">Exported the SSL certificate</span></span>
> * <span data-ttu-id="3ccdb-159">Ha aprendido a usar el certificado en Java, Python y Node.js</span><span class="sxs-lookup"><span data-stu-id="3ccdb-159">Learned how to use the certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="3ccdb-160">Ahora puede continuar a la sección de conceptos para obtener más información sobre Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3ccdb-160">You can now proceed to the Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ccdb-161">Distribución global</span><span class="sxs-lookup"><span data-stu-id="3ccdb-161">Global distribution</span></span>](distribute-data-globally.md) 
