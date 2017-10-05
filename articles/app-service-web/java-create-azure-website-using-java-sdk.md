---
title: "Creación de una aplicación web en el Servicio de aplicaciones de Azure mediante el SDK de Azure para Java"
description: "Obtenga información acerca de cómo crear una aplicación web en el Servicio de aplicaciones de Azure mediante programación usando el SDK de Azure para Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="cde34-103">Creación de una aplicación web en el Servicio de aplicaciones de Azure mediante el SDK de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="cde34-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="cde34-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cde34-104">Overview</span></span>
<span data-ttu-id="cde34-105">En este tutorial se muestra cómo crear una instancia de Azure SDK para la aplicación Java que crea una aplicación web en [Azure App Service][Azure App Service]. A continuación, se explica cómo implementar una aplicación en ella.</span><span class="sxs-lookup"><span data-stu-id="cde34-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="cde34-106">Consta de dos partes:</span><span class="sxs-lookup"><span data-stu-id="cde34-106">It consists of two parts:</span></span>

* <span data-ttu-id="cde34-107">En la parte 1, se describe cómo crear una aplicación Java que crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="cde34-108">En la parte 2, se explica cómo crear una aplicación JSP sencilla ("Hello World") y, a continuación, se describe el uso de un cliente FTP para implementar código en un servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cde34-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cde34-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cde34-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="cde34-110">Instalaciones de software</span><span class="sxs-lookup"><span data-stu-id="cde34-110">Software Installations</span></span>
<span data-ttu-id="cde34-111">El código de aplicación de AzureWebDemo de este artículo se escribió con el SDK 0.7.0 de Azure Java, que se instala mediante el [instalador de plataforma web (WebPI)][Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="cde34-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="cde34-112">Además, asegúrese de utilizar la versión más reciente del [kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cde34-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="cde34-113">Después de instalar el SDK, actualice las dependencias del proyecto de Eclipse ejecutando **Update index** (Actualizar índice) en **Maven Repositories** (Repositorios de Maven). A continuación, vuelva a agregar la versión más reciente de cada paquete en la ventana **Dependencies** (Dependencias).</span><span class="sxs-lookup"><span data-stu-id="cde34-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="cde34-114">Para comprobar la versión del software instalado en Eclipse, haga clic en **Help (Ayuda) > Installation Details (Detalles de la instalación)**. Debe tener al menos las siguientes versiones:</span><span class="sxs-lookup"><span data-stu-id="cde34-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="cde34-115">Paquete para bibliotecas de Microsoft Azure para Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="cde34-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="cde34-116">IDE de Eclipse para desarrolladores de Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="cde34-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="cde34-117">Creación y configuración de recursos en la nube en Azure</span><span class="sxs-lookup"><span data-stu-id="cde34-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="cde34-118">Antes de comenzar este procedimiento, debe tener una suscripción activa de Azure y configurar un Active Directory (AD) predeterminado en Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="cde34-119">Creación de un Active Directory (AD) en Azure</span><span class="sxs-lookup"><span data-stu-id="cde34-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="cde34-120">Si no tiene todavía un Active Directory (AD) en su suscripción de Azure, inicie sesión en el [Portal de Azure clásico][Azure classic portal] con su cuenta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cde34-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="cde34-121">Si tiene varias suscripciones, haga clic en **Suscripciones** y elija el directorio predeterminado de la suscripción que desee usar en este proyecto.</span><span class="sxs-lookup"><span data-stu-id="cde34-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="cde34-122">A continuación, haga clic en **Aplicar** para acceder a esa vista de suscripción.</span><span class="sxs-lookup"><span data-stu-id="cde34-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="cde34-123">Elija **Active Directory** en el menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="cde34-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="cde34-124">Haga clic en **Nuevo > Directorio > Creación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="cde34-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="cde34-125">En **Agregar directorio**, elija **Crear nuevo directorio**.</span><span class="sxs-lookup"><span data-stu-id="cde34-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="cde34-126">En **Nombre**, escriba un nombre para el directorio.</span><span class="sxs-lookup"><span data-stu-id="cde34-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="cde34-127">En **Dominio**, escriba un nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="cde34-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="cde34-128">Se trata de un nombre de dominio básico que se incluye de forma predeterminada en el directorio. Tiene el formato `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="cde34-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="cde34-129">Puede asignarle un nombre basado en el nombre del directorio o en otro nombre de dominio que posea.</span><span class="sxs-lookup"><span data-stu-id="cde34-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="cde34-130">Más adelante, puede agregar otro nombre de dominio que ya use su organización.</span><span class="sxs-lookup"><span data-stu-id="cde34-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="cde34-131">En **País o región**, elija la configuración regional que corresponda.</span><span class="sxs-lookup"><span data-stu-id="cde34-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="cde34-132">Para obtener más información sobre AD, consulte [¿Qué es un directorio de Azure AD?][What is an Azure AD directory]</span><span class="sxs-lookup"><span data-stu-id="cde34-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="cde34-133">Creación de un certificado de administración para Azure</span><span class="sxs-lookup"><span data-stu-id="cde34-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="cde34-134">El SDK de Azure para Java usa certificados de administración para autenticar con las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="cde34-135">Se trata de certificados X.509 v3 que se utilizan para autenticar una aplicación cliente que utiliza la API de administración de servicios para actuar en nombre del propietario de la suscripción a fin de administrar los recursos de suscripción.</span><span class="sxs-lookup"><span data-stu-id="cde34-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="cde34-136">El código de este procedimiento utiliza un certificado autofirmado para autenticarse con Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="cde34-137">Para este procedimiento, deberá crear un certificado y cargarlo previamente en el [Portal de Azure clásico][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="cde34-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="cde34-138">Esto implica los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cde34-138">This involves the following steps:</span></span>

* <span data-ttu-id="cde34-139">Generar un archivo PFX que represente el certificado de cliente y guardarlo localmente.</span><span class="sxs-lookup"><span data-stu-id="cde34-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="cde34-140">Generar un certificado de administración (archivo CER) a partir del archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="cde34-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="cde34-141">Cargar el archivo CER en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="cde34-142">Convertir el archivo PFX en JKS, ya que Java utiliza ese formato para la autenticación mediante certificados.</span><span class="sxs-lookup"><span data-stu-id="cde34-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="cde34-143">Escribir el código de autenticación de la aplicación, que hace referencia al archivo JKS local.</span><span class="sxs-lookup"><span data-stu-id="cde34-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="cde34-144">Al completar este procedimiento, el certificado CER residirá en su suscripción de Azure y el certificado JKS, en la unidad local.</span><span class="sxs-lookup"><span data-stu-id="cde34-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="cde34-145">Para obtener más información sobre la administración de certificados, consulte [Crear y cargar un certificado de administración para Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cde34-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="cde34-146">Creación de un certificado</span><span class="sxs-lookup"><span data-stu-id="cde34-146">Create a certificate</span></span>
<span data-ttu-id="cde34-147">Para crear su propio certificado autofirmado, abra una consola de comandos en el sistema operativo y ejecute los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="cde34-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="cde34-148">**Nota:** El equipo en el que se ejecute este comando debe tener instalado el JDK.</span><span class="sxs-lookup"><span data-stu-id="cde34-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="cde34-149">Además, la ruta a la herramienta de generación de claves (keytool) depende de la ubicación en la que se instale el JDK.</span><span class="sxs-lookup"><span data-stu-id="cde34-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="cde34-150">Para obtener más información, consulte [Keytool: herramienta para administrar certificados y claves][Key and Certificate Management Tool (keytool)] en la documentación en línea de Java.</span><span class="sxs-lookup"><span data-stu-id="cde34-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="cde34-151">Para crear el archivo .pfx:</span><span class="sxs-lookup"><span data-stu-id="cde34-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="cde34-152">Para crear el archivo .cer:</span><span class="sxs-lookup"><span data-stu-id="cde34-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="cde34-153">donde:</span><span class="sxs-lookup"><span data-stu-id="cde34-153">where:</span></span>

* <span data-ttu-id="cde34-154">`<java-install-dir>` es la ruta al directorio donde se instaló Java.</span><span class="sxs-lookup"><span data-stu-id="cde34-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="cde34-155">`<keystore-id>` es el identificador de entrada del almacén de claves (por ejemplo, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="cde34-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="cde34-156">`<cert-store-dir>` es la ruta al directorio en el que desea almacenar los certificados (por ejemplo, `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="cde34-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="cde34-157">`<cert-file-name>` es el nombre del archivo de certificado (por ejemplo, `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="cde34-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="cde34-158">`<password>` es la contraseña elegida para proteger el certificado. Debe tener 6 caracteres como mínimo.</span><span class="sxs-lookup"><span data-stu-id="cde34-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="cde34-159">Se puede optar por no escribir ninguna contraseña, aunque no se recomienda.</span><span class="sxs-lookup"><span data-stu-id="cde34-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="cde34-160">`<dname>` es el nombre distintivo X.500 que debe asociarse con el alias. Se utiliza en los campos del asunto y del emisor en el certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="cde34-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="cde34-161">Para obtener más información, consulte [Crear y cargar un certificado de administración para Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cde34-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="cde34-162">Carga del certificado</span><span class="sxs-lookup"><span data-stu-id="cde34-162">Upload the certificate</span></span>
<span data-ttu-id="cde34-163">Para cargar un certificado autofirmado en Azure, vaya a la página **Configuración** en el portal de clásico. A continuación, haga clic en la pestaña **Certificados de administración**. Haga clic en **Cargar**, en la parte inferior de la página, y desplácese hasta la ubicación del archivo CER que creó previamente.</span><span class="sxs-lookup"><span data-stu-id="cde34-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="cde34-164">Conversión del archivo PFX en JKS</span><span class="sxs-lookup"><span data-stu-id="cde34-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="cde34-165">Como administrador, acceda al símbolo del sistema de Windows. Cambie al directorio que contiene los certificados y ejecute el comando siguiente, donde `<java-install-dir>` es el directorio donde instaló Java en su equipo:</span><span class="sxs-lookup"><span data-stu-id="cde34-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="cde34-166">Cuando se le pida, escriba la contraseña del almacén de claves de destino. Se trata de la contraseña para el archivo JKS.</span><span class="sxs-lookup"><span data-stu-id="cde34-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="cde34-167">Cuando se le pida, escriba la contraseña del almacén de claves de origen. Esta es la contraseña que especificó para el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="cde34-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="cde34-168">Las dos contraseñas no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="cde34-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="cde34-169">Se puede optar por no escribir ninguna contraseña, aunque no se recomienda.</span><span class="sxs-lookup"><span data-stu-id="cde34-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="cde34-170">Compilación de una aplicación para crear aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="cde34-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="cde34-171">Creación del área de trabajo de Eclipse y el proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="cde34-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="cde34-172">En esta sección, creará un área de trabajo y un proyecto de Maven para la aplicación de creación de aplicaciones web, denominada AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="cde34-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="cde34-173">Cree un nuevo proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="cde34-173">Create a new Maven project.</span></span> <span data-ttu-id="cde34-174">Haga clic en **File (Archivo) > New (Nuevo) > Maven Project (Proyecto de Maven)**.</span><span class="sxs-lookup"><span data-stu-id="cde34-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="cde34-175">En **New Maven Project** (Nuevo proyecto de Maven), elija **Create a simple project** (Crear proyecto sencillo) y, a continuación, elija **Use default workspace location** (Usar ubicación de espacio de trabajo predeterminada).</span><span class="sxs-lookup"><span data-stu-id="cde34-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="cde34-176">En la segunda página de **New Maven Project**(Nuevo proyecto de Maven), especifique lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cde34-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="cde34-177">Group ID (Identificador del grupo): `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="cde34-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="cde34-178">Artifact ID (Identificador de artefacto): AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="cde34-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="cde34-179">Version (Versión): 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="cde34-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="cde34-180">Packaging (Empaquetado): jar</span><span class="sxs-lookup"><span data-stu-id="cde34-180">Packaging: jar</span></span>
   * <span data-ttu-id="cde34-181">Name (Nombre): AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="cde34-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="cde34-182">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cde34-182">Click **Finish**.</span></span>
3. <span data-ttu-id="cde34-183">Abra el nuevo archivo pom.xml del proyecto en el Explorador de proyectos.</span><span class="sxs-lookup"><span data-stu-id="cde34-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="cde34-184">Elija la pestaña **Dependencies** (Dependencias). Como se trata de un nuevo proyecto, todavía no se muestra ningún paquete.</span><span class="sxs-lookup"><span data-stu-id="cde34-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="cde34-185">Abra la vista Maven Repositories (Repositorios de Maven).</span><span class="sxs-lookup"><span data-stu-id="cde34-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="cde34-186">**Haga clic en Window (Ventana) > Show View (Mostrar vista) > Other (Otro) > Maven > Maven Repositories (Repositorios de Maven)** y luego en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="cde34-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="cde34-187">La vista **Maven Repositories** (Repositorios de Maven) aparece en la parte inferior de IDE.</span><span class="sxs-lookup"><span data-stu-id="cde34-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="cde34-188">Abra **Global Repositories** (Repositorios globales), haga clic con el botón derecho en el repositorio **Central** y elija **Rebuild Index** (Volver a generar el índice).</span><span class="sxs-lookup"><span data-stu-id="cde34-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="cde34-189">Este paso puede tardar varios minutos, según la velocidad de la conexión.</span><span class="sxs-lookup"><span data-stu-id="cde34-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="cde34-190">Cuando se vuelve a generar el índice, deberían mostrarse los paquetes de Microsoft Azure en el repositorio **central** de Maven.</span><span class="sxs-lookup"><span data-stu-id="cde34-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="cde34-191">En **Dependencies** (Dependencias), haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="cde34-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="cde34-192">En **Enter Group ID...** (Especificar identificador de grupo), escriba `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="cde34-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="cde34-193">Elija los paquetes para la administración de base y la administración de aplicaciones web del Servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="cde34-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="cde34-194">**Nota:** si va a actualizar las dependencias después de que se haya lanzado una nueva versión, tendrá que volver a agregar cada una de las dependencias en esta lista.</span><span class="sxs-lookup"><span data-stu-id="cde34-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="cde34-195">Después de hacer clic en **Add** (Agregar) y elegir cada dependencia, esta aparece con el nuevo número de versión en la lista **Dependencies** (Dependencias).</span><span class="sxs-lookup"><span data-stu-id="cde34-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="cde34-196">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-196">Click **OK**.</span></span> <span data-ttu-id="cde34-197">Los paquetes de Azure aparecen entonces en la lista **Dependencies** (Dependencias).</span><span class="sxs-lookup"><span data-stu-id="cde34-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="cde34-198">Escritura de código Java para crear una aplicación web mediante una llamada al SDK de Azure</span><span class="sxs-lookup"><span data-stu-id="cde34-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="cde34-199">A continuación, escriba el código que efectúa la llamada a las API en el SDK de Azure para que Java cree la aplicación web de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cde34-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="cde34-200">Cree una clase de Java que contenga el código de punto de entrada principal.</span><span class="sxs-lookup"><span data-stu-id="cde34-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="cde34-201">En el Explorador de proyectos, haga clic con el botón derecho en el nodo del proyecto y elija **Nueva (Nuevo) > Clase (Clase)**.</span><span class="sxs-lookup"><span data-stu-id="cde34-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="cde34-202">En **New Java Class** (Nueva clase de Java) asigne un nombre a la clase `WebCreator` y active la casilla **public static void main**.</span><span class="sxs-lookup"><span data-stu-id="cde34-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="cde34-203">Las selecciones deberían aparecer de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="cde34-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="cde34-204">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cde34-204">Click **Finish**.</span></span> <span data-ttu-id="cde34-205">El archivo WebCreator.java aparece en el Explorador de proyectos.</span><span class="sxs-lookup"><span data-stu-id="cde34-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="cde34-206">Llamada a la API de Azure para crear una aplicación web de Servicio de la aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cde34-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="cde34-207">Adición de las importaciones necesarias</span><span class="sxs-lookup"><span data-stu-id="cde34-207">Add necessary imports</span></span>
<span data-ttu-id="cde34-208">En WebCreator.java, agregue las siguientes importaciones. Estas importaciones proporcionan acceso a las clases en las bibliotecas de administración para utilizar las API de Azure:</span><span class="sxs-lookup"><span data-stu-id="cde34-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="cde34-209">Definición de la clase de punto de entrada principal</span><span class="sxs-lookup"><span data-stu-id="cde34-209">Define the main entry point class</span></span>
<span data-ttu-id="cde34-210">Dado que el propósito de la aplicación AzureWebDemo es crear una aplicación web de Servicio de aplicaciones, asigne un nombre a la clase principal para esta aplicación `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="cde34-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="cde34-211">Esta clase proporciona el código de punto de entrada principal que efectúa la llamada a la API de administración de Servicios de Azure para crear la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="cde34-212">Agregue las siguientes definiciones de parámetros para la aplicación web y el espacio web.</span><span class="sxs-lookup"><span data-stu-id="cde34-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="cde34-213">Deberá proporcionar su propia información de certificado y de identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="cde34-214">donde:</span><span class="sxs-lookup"><span data-stu-id="cde34-214">where:</span></span>

* <span data-ttu-id="cde34-215">`<subscription-id>` es el identificador de suscripción de Azure en el que desea crear el recurso.</span><span class="sxs-lookup"><span data-stu-id="cde34-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="cde34-216">`<certificate-store-path>` es la ruta y el nombre de archivo del archivo JKS en el directorio del almacén de certificados local.</span><span class="sxs-lookup"><span data-stu-id="cde34-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="cde34-217">Por ejemplo, `C:/Certificates/CertificateName.jks` para Linux y `C:\Certificates\CertificateName.jks` para Windows.</span><span class="sxs-lookup"><span data-stu-id="cde34-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="cde34-218">`<certificate-password>` es la contraseña que se especificó al crear el certificado de JKS.</span><span class="sxs-lookup"><span data-stu-id="cde34-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="cde34-219">`webAppName` puede ser cualquier nombre que elija. En este procedimiento, se utiliza el nombre `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="cde34-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="cde34-220">El nombre de dominio completo es la `webAppName` con el `domainName` anexado, por lo que, en este caso, el dominio completo es `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cde34-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="cde34-221">`domainName` debe especificarse del modo indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cde34-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="cde34-222">`webSpaceName` debe ser uno de los valores definidos en la clase [WebSpaceNames][WebSpaceNames].</span><span class="sxs-lookup"><span data-stu-id="cde34-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="cde34-223">`appServicePlanName` debe especificarse del modo indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cde34-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="cde34-224">**Nota:** Cada vez que ejecute esta aplicación, deberá cambiar el valor de `webAppName` y `appServicePlanName` (o eliminar la aplicación web en Azure Portal) antes de ejecutar la aplicación de nuevo.</span><span class="sxs-lookup"><span data-stu-id="cde34-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="cde34-225">De lo contrario, se producirá un error de ejecución porque ya existe el mismo recurso en Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="cde34-226">Definición del método de creación web</span><span class="sxs-lookup"><span data-stu-id="cde34-226">Define the web creation method</span></span>
<span data-ttu-id="cde34-227">A continuación, defina un método para crear la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="cde34-228">Este método, `createWebApp`, especifica los parámetros de la aplicación web y el espacio web.</span><span class="sxs-lookup"><span data-stu-id="cde34-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="cde34-229">También crea y configura el cliente de administración de aplicaciones web de App Service Web Apps, que se define mediante el objeto [WebSiteManagementClient][WebSiteManagementClient].</span><span class="sxs-lookup"><span data-stu-id="cde34-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="cde34-230">El cliente de administración es fundamental para crear aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="cde34-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="cde34-231">Proporciona servicios web RESTful que permiten a las aplicaciones administrar aplicaciones web (realizar operaciones tales como crear, actualizar y eliminar) mediante una llamada a la API de administración de servicios.</span><span class="sxs-lookup"><span data-stu-id="cde34-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="cde34-232">El código dará como resultado el estado de HTTP de la respuesta indicando si es correcto o erróneo. Si es correcto, se generará el nombre de la aplicación web creada.</span><span class="sxs-lookup"><span data-stu-id="cde34-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="cde34-233">Definición del método main()</span><span class="sxs-lookup"><span data-stu-id="cde34-233">Define the main() method</span></span>
<span data-ttu-id="cde34-234">Especifique el código del método main() que efectúa la llamada a createWebApp() para crear la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="cde34-235">Por último, efectúe una llamada a `createWebApp` desde `main`:</span><span class="sxs-lookup"><span data-stu-id="cde34-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="cde34-236">Ejecución de la aplicación y verificación de la creación de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="cde34-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="cde34-237">Para verificar que la aplicación puede ejecutarse, haga clic en **Ejecutar > Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="cde34-238">Cuando la aplicación complete la ejecución, verá el siguiente resultado en la consola de Eclipse:</span><span class="sxs-lookup"><span data-stu-id="cde34-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="cde34-239">Inicie sesión en el portal clásico de Azure y haga clic en **Aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="cde34-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cde34-240">La nueva aplicación web debería aparecer en la lista Aplicaciones web dentro de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="cde34-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="cde34-241">Implementación de una aplicación en la aplicación web</span><span class="sxs-lookup"><span data-stu-id="cde34-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="cde34-242">Después de ejecutar AzureWebDemo y crear la nueva aplicación web, inicie sesión en el portal clásico, haga clic en **Aplicaciones web** y elija **WebDemoWebApp** en la lista **Aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="cde34-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="cde34-243">En la página del panel de la aplicación web, haga clic en **Examinar** (o en la dirección URL, `webdemowebapp.azurewebsites.net`) para acceder a ella.</span><span class="sxs-lookup"><span data-stu-id="cde34-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="cde34-244">Se mostrará una página con un marcador de posición en blanco, porque todavía no hay contenido publicado en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="cde34-245">A continuación, creará una aplicación "Hello World" y la implementará en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="cde34-246">Creación de una aplicación Hello World en JSP</span><span class="sxs-lookup"><span data-stu-id="cde34-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="cde34-247">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cde34-247">Create the application</span></span>
<span data-ttu-id="cde34-248">Para demostrar cómo se implementa una aplicación en la web, el siguiente procedimiento describe cómo se crea una aplicación "Hello World" sencilla de Java y cómo se carga en la aplicación web del Servicio de aplicaciones que se creó con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cde34-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="cde34-249">Haga clic en **File (Archivo) > New (Nuevo) > Dynamic Web Project (Proyecto web dinámico)**.</span><span class="sxs-lookup"><span data-stu-id="cde34-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="cde34-250">Asígnele el nombre `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="cde34-250">Name it `JSPHello`.</span></span> <span data-ttu-id="cde34-251">No es necesario cambiar ninguna otra configuración en este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cde34-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="cde34-252">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cde34-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="cde34-253">En el Explorador de proyectos, expanda el proyecto **JSPHello**, haga clic con el botón derecho en **WebContent**. A continuación, haga clic en **New (Nuevo) > JSP File (Archivo JSP)**.</span><span class="sxs-lookup"><span data-stu-id="cde34-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="cde34-254">En el cuadro de diálogo Nuevo archivo JSP, asigne al archivo el nombre `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="cde34-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="cde34-255">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cde34-255">Click **Next**.</span></span>
3. <span data-ttu-id="cde34-256">En el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), seleccione **New JSP File (html)** [Nuevo archivo JSP (htlm)] y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="cde34-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="cde34-257">En index.jsp, agregue el siguiente código en las secciones de las etiquetas `<head>` y `<body>`:</span><span class="sxs-lookup"><span data-stu-id="cde34-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="cde34-258">Ejecución de la aplicación Hello World en el host local</span><span class="sxs-lookup"><span data-stu-id="cde34-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="cde34-259">Antes de ejecutar esta aplicación, deberá configurar algunas propiedades.</span><span class="sxs-lookup"><span data-stu-id="cde34-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="cde34-260">Haga clic con el botón derecho en el proyecto **JSPHello** y elija **Properties** (Propiedades).</span><span class="sxs-lookup"><span data-stu-id="cde34-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="cde34-261">En el cuadro de diálogo **Propiedades** (Propiedades), elija **Java Build Path** (Ruta de compilación de Java), elija la pestaña **Order and Export** (Ordenar y exportar), elija **JRE System Library** (Biblioteca del sistema JRE), a continuación, haga clic en **Up** (Arriba) para moverla a la parte superior de la lista.</span><span class="sxs-lookup"><span data-stu-id="cde34-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="cde34-262">También, en el cuadro de diálogo **Propiedades** (Propiedades), elija **Targeted Runtimes** (Tiempo de ejecución de destino) y haga clic en **New** (Nuevo).</span><span class="sxs-lookup"><span data-stu-id="cde34-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="cde34-263">En el cuadro de diálogo **New Server Runtime Environment** (Entorno de ejecución del nuevo servidor), elija un servidor, como **Apache Tomcat v7.0**, y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="cde34-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="cde34-264">En el cuadro de diálogo **Tomcat Server** (Servidor de Tomcat), configure el valor de **Name** (Nombre) en `Apache Tomcat v7.0` y establezca **Tomcat Installation Directory** (Directorio de instalación de Tomcat) en el directorio en el que se instaló la versión del servidor de Tomcat que desea usar.</span><span class="sxs-lookup"><span data-stu-id="cde34-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="cde34-265">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cde34-265">Click **Finish**.</span></span>
5. <span data-ttu-id="cde34-266">Volverá a la página **Targeted Runtimes** (Tiempo de ejecución de destino) del cuadro de diálogo **Properties** (Propiedades).</span><span class="sxs-lookup"><span data-stu-id="cde34-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="cde34-267">Elija **Apache Tomcat v7.0** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="cde34-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="cde34-268">En Eclipse, en el menú **Run** (Ejecutar), haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="cde34-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="cde34-269">En el cuadro de diálogo **Run As** (Ejecutar como), elija **Run on Server** (Ejecutar en el servidor).</span><span class="sxs-lookup"><span data-stu-id="cde34-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="cde34-270">En el cuadro de diálogo **Run on Server** (Ejecutar en el servidor), elija **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="cde34-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="cde34-271">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cde34-271">Click **Finish**.</span></span>
7. <span data-ttu-id="cde34-272">Cuando se ejecute la aplicación, la página **JSPHello** debería aparecer en una ventana del host local en Eclipse (`http://localhost:8080/JSPHello/`), con el mensaje siguiente:</span><span class="sxs-lookup"><span data-stu-id="cde34-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="cde34-273">Exportación de la aplicación como WAR</span><span class="sxs-lookup"><span data-stu-id="cde34-273">Export the application as a WAR</span></span>
<span data-ttu-id="cde34-274">Exporte los archivos de proyecto web como un archivo web (WAR) para que pueda implementarlo en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="cde34-275">Los siguientes archivos del proyecto web residen en la carpeta WebContent:</span><span class="sxs-lookup"><span data-stu-id="cde34-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="cde34-276">Haga clic con el botón derecho en la carpeta WebContent y elija **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="cde34-277">En el cuadro de diálogo **Exportar selección**, haga clic en **Web > WAR**. Después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cde34-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="cde34-278">En el cuadro de diálogo **Exportar WAR** , elija el directorio de origen del proyecto actual e incluya el nombre del archivo WAR al final.</span><span class="sxs-lookup"><span data-stu-id="cde34-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="cde34-279">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cde34-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="cde34-280">Para obtener más información sobre cómo implementar archivos WAR, consulte [Adición de una aplicación Java a las aplicaciones web del Servicio de aplicaciones de Azure](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="cde34-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="cde34-281">Implementación de la aplicación Hello World mediante FTP</span><span class="sxs-lookup"><span data-stu-id="cde34-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="cde34-282">Elija un cliente FTP de terceros para publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cde34-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="cde34-283">En este procedimiento, se describen dos opciones: la consola Kudu integrada en Azure y FileZilla, una herramienta popular con una cómoda interfaz de usuario gráfica.</span><span class="sxs-lookup"><span data-stu-id="cde34-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="cde34-284">**Nota:** el Kit de herramientas de Azure para Eclipse admite la implementación en cuentas de almacenamiento y servicios en la nube, pero no admite actualmente la implementación en aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="cde34-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="cde34-285">Puede realizar implementaciones en cuentas de almacenamiento y servicios en la nube mediante un proyecto de implementación de Azure, tal y como se describe en [Creación de una aplicación Hola a todos para Azure en Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), pero no en aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="cde34-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="cde34-286">Utilice otros métodos, como GitHub o FTP, para transferir archivos a su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="cde34-287">**Nota:** no se recomienda utilizar FTP desde el símbolo del sistema de Windows (la utilidad línea de comandos FTP.EXE que se incluye con Windows).</span><span class="sxs-lookup"><span data-stu-id="cde34-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="cde34-288">Los clientes FTP que utilizan FTP activo, como FTP.EXE, a menudo no funcionan a través de firewalls.</span><span class="sxs-lookup"><span data-stu-id="cde34-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="cde34-289">El FTP activo especifica una dirección interna basada en LAN a la que es difícil que pueda conectarse un servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="cde34-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="cde34-290">Para obtener más información acerca de la implementación en una aplicación web del Servicio de aplicaciones mediante FTP, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="cde34-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="cde34-291">Implementación mediante una utilidad FTP</span><span class="sxs-lookup"><span data-stu-id="cde34-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="cde34-292">Configurar credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="cde34-292">Set up deployment credentials</span></span>
<span data-ttu-id="cde34-293">Debe haber ejecutado la aplicación **AzureWebDemo** para crear una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="cde34-294">Los archivos se transfieren a esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="cde34-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="cde34-295">Inicie sesión en el portal clásico y haga clic en **Aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="cde34-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cde34-296">Asegúrese de que **WebDemoWebApp** aparezca en la lista de aplicaciones web y de que esté en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cde34-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="cde34-297">Haga clic en **WebDemoWebApp** para abrir la página **Panel**.</span><span class="sxs-lookup"><span data-stu-id="cde34-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="cde34-298">En la página **Panel**, en **Vista rápida**, haga clic en **Configurar credenciales de implementación** (si ya cuenta con credenciales de implementación, la opción será **Restablecer credenciales de implementación**).</span><span class="sxs-lookup"><span data-stu-id="cde34-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="cde34-299">Credenciales de implementación asociadas con una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cde34-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="cde34-300">Deberá especificar un nombre de usuario y una contraseña que pueda utilizar para realizar la implementación con Git y FTP.</span><span class="sxs-lookup"><span data-stu-id="cde34-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="cde34-301">Puede usar estas credenciales para la implementación en cualquier aplicación web en todas las suscripciones de Azure asociadas a su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cde34-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="cde34-302">Especifique las credenciales de implementación de Git y FTP en el cuadro de diálogo. Tome nota del nombre de usuario y la contraseña para usarlos en el futuro.</span><span class="sxs-lookup"><span data-stu-id="cde34-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="cde34-303">Obtención de la información de conexión para FTP</span><span class="sxs-lookup"><span data-stu-id="cde34-303">Get FTP connection information</span></span>
<span data-ttu-id="cde34-304">Si desea utilizar FTP para implementar archivos de aplicación en la aplicación web recién creada, deberá obtener información de conexión.</span><span class="sxs-lookup"><span data-stu-id="cde34-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="cde34-305">Hay dos maneras de obtener información de conexión.</span><span class="sxs-lookup"><span data-stu-id="cde34-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="cde34-306">Una de ellas es visitar la página **Panel** de la aplicación web. La otra manera es descargar el perfil de publicación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="cde34-307">El perfil de publicación es un archivo XML que proporciona información como las credenciales de inicio de sesión y el nombre de host FTP para sus aplicaciones web en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="cde34-308">Puede usar este nombre de usuario y contraseña para realizar la implementación en cualquier aplicación web en todas las suscripciones asociadas a la cuenta de Azure y no únicamente esta.</span><span class="sxs-lookup"><span data-stu-id="cde34-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="cde34-309">Para obtener información de conexión de FTP a partir de las hojas de la aplicación web en [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="cde34-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="cde34-310">En **Essentials**, busque y copie **Nombre de host de FTP**.</span><span class="sxs-lookup"><span data-stu-id="cde34-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="cde34-311">Se trata de un URI similar a `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="cde34-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="cde34-312">En **Essentials**, busque y copie **FTP/Nombre de usuario de implementación**.</span><span class="sxs-lookup"><span data-stu-id="cde34-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="cde34-313">Tendrá el formato *nombreaplicaciónweb\nombreusuarioimplementación*, por ejemplo `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="cde34-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="cde34-314">Para obtener información sobre la conexión FTP desde el perfil de publicación:</span><span class="sxs-lookup"><span data-stu-id="cde34-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="cde34-315">En la hoja de la aplicación web, haga clic en **Obtener perfil de publicación**.</span><span class="sxs-lookup"><span data-stu-id="cde34-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="cde34-316">Se descargará un archivo .publishsettings en la unidad local.</span><span class="sxs-lookup"><span data-stu-id="cde34-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="cde34-317">Abra el archivo .publishsettings en un editor XML o un editor de texto y busque el elemento `<publishProfile>` que contiene `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="cde34-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="cde34-318">Debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="cde34-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="cde34-319">Tenga en cuenta que la configuración `publishProfile` de la aplicación web se asigna a la configuración del administrador del sitio de FileZilla de esta forma:</span><span class="sxs-lookup"><span data-stu-id="cde34-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="cde34-320">`publishUrl` es el mismo valor que el **Nombre de host de FTP**, el valor establecido en **Host**.</span><span class="sxs-lookup"><span data-stu-id="cde34-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="cde34-321">`publishMethod="FTP"` significa que se establece el valor **Protocolo** en **FTP - Protocolo de transferencia de archivos**. El valor de **Cifrado** debe ser **Usar FTP sin formato**.</span><span class="sxs-lookup"><span data-stu-id="cde34-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="cde34-322">`userName` y `userPWD` son claves para los valores reales del nombre de usuario y la contraseña que especificó al restablecer las credenciales de la implementación.</span><span class="sxs-lookup"><span data-stu-id="cde34-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="cde34-323">`userName` es el mismo que **Implementación/Usuario FTP**.</span><span class="sxs-lookup"><span data-stu-id="cde34-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="cde34-324">Se asignan a **Usuario** y **Contraseña** en FileZilla.</span><span class="sxs-lookup"><span data-stu-id="cde34-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="cde34-325">`ftpPassiveMode="True"` significa que el sitio FTP utiliza la transferencia FTP pasiva. Elija **Pasivo** en la pestaña **Opciones de Transferencia**.</span><span class="sxs-lookup"><span data-stu-id="cde34-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="cde34-326">Configuración de la aplicación web para hospedar una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="cde34-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="cde34-327">Antes de publicar la aplicación, deberá cambiar algunos valores de configuración para que la aplicación web pueda hospedar una aplicación Java.</span><span class="sxs-lookup"><span data-stu-id="cde34-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="cde34-328">En el portal clásico, vaya a la página **Panel** de la aplicación web y haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="cde34-329">En la página **Configurar** , especifique la configuración siguiente.</span><span class="sxs-lookup"><span data-stu-id="cde34-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="cde34-330">En **Versión de Java**, el valor predeterminado es **Desactivar**. Elija la versión de Java a la que se dirige su aplicación, por ejemplo 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="cde34-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="cde34-331">Después de esto, asegúrese de que **Contenedor web** esté establecido en una versión del servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cde34-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="cde34-332">En **Documentos predeterminados**, agregue index.jsp y colóquelo en la parte superior de la lista.</span><span class="sxs-lookup"><span data-stu-id="cde34-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="cde34-333">(El archivo predeterminado para las aplicaciones web es hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="cde34-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="cde34-334">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="cde34-335">Publicación de la aplicación mediante Kudu</span><span class="sxs-lookup"><span data-stu-id="cde34-335">Publish your application using Kudu</span></span>
<span data-ttu-id="cde34-336">Una manera de publicar la aplicación consiste en utilizar la consola de depuración Kudu integrada en Azure.</span><span class="sxs-lookup"><span data-stu-id="cde34-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="cde34-337">Kudu es conocido por su estabilidad y coherencia con las aplicaciones web del Servicio de aplicaciones y el servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cde34-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="cde34-338">Puede obtener acceso a la consola para la aplicación web a través de una dirección URL de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="cde34-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="cde34-339">Para este procedimiento, la consola Kudu se encuentra en la siguiente dirección URL. Acceda a esta ubicación:</span><span class="sxs-lookup"><span data-stu-id="cde34-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="cde34-340">En el menú superior, elija **Consola de depuración > CMD**.</span><span class="sxs-lookup"><span data-stu-id="cde34-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="cde34-341">En la línea de comandos de la consola, vaya a `/site/wwwroot` (o haga clic en `site` y en `wwwroot`, en la parte superior de la página de la vista de directorios):</span><span class="sxs-lookup"><span data-stu-id="cde34-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="cde34-342">Después de especificar un valor en **Versión de Java**, el servidor de Tomcat debe crear un directorio de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="cde34-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="cde34-343">En la línea de comandos de la consola, acceda al directorio de aplicaciones web:</span><span class="sxs-lookup"><span data-stu-id="cde34-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="cde34-344">Arrastre JSPHello.war desde `<project-path>/JSPHello/src/` y colóquelo en la vista de directorio Kudu, en `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cde34-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cde34-345">No lo arrastre hasta el área "Arrastre aquí para cargar y comprimir", porque Tomcat lo descomprimirá.</span><span class="sxs-lookup"><span data-stu-id="cde34-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="cde34-346">En primer lugar, JSPHello.war aparece en el área de directorio por sí solo:</span><span class="sxs-lookup"><span data-stu-id="cde34-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="cde34-347">Poco tiempo después (probablemente, menos de 5 minutos), el servidor de Tomcat descomprimirá el archivo WAR en un directorio JSPHello desempaquetado.</span><span class="sxs-lookup"><span data-stu-id="cde34-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="cde34-348">Haga clic en el directorio raíz para ver si index.jsp se ha descomprimido y copiado allí.</span><span class="sxs-lookup"><span data-stu-id="cde34-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="cde34-349">Si es así, acceda de nuevo al directorio de aplicaciones web para ver si se ha creado el directorio JSPHello desempaquetado.</span><span class="sxs-lookup"><span data-stu-id="cde34-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="cde34-350">Si no ve estos elementos, espere y repita el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="cde34-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="cde34-351">Publicación de la aplicación mediante FileZilla (opcional)</span><span class="sxs-lookup"><span data-stu-id="cde34-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="cde34-352">Otra herramienta que puede usar para publicar la aplicación es FileZilla, un cliente FTP de terceros popular con una cómoda interfaz de usuario gráfica.</span><span class="sxs-lookup"><span data-stu-id="cde34-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="cde34-353">Puede descargar e instalar FileZilla desde [http://filezilla-project.org/](http://filezilla-project.org/) en caso de que no lo tenga.</span><span class="sxs-lookup"><span data-stu-id="cde34-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="cde34-354">Para más información sobre cómo utilizar el cliente, consulte la [documentación de FileZilla](https://wiki.filezilla-project.org/Documentation) y esta entrada de blog en [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx) (Clientes FTP - Parte 4: FileZilla).</span><span class="sxs-lookup"><span data-stu-id="cde34-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="cde34-355">En FileZilla, haga clic en **Archivo > Gestor de sitios**.</span><span class="sxs-lookup"><span data-stu-id="cde34-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="cde34-356">En el cuadro de diálogo **Gestor de sitios**, haga clic en **Nuevo sitio**.</span><span class="sxs-lookup"><span data-stu-id="cde34-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="cde34-357">Aparecerá un nuevo sitio FTP en blanco en **Select Entry** (Seleccionar entrada), en el que se le solicitará que proporcione un nombre.</span><span class="sxs-lookup"><span data-stu-id="cde34-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="cde34-358">Para este procedimiento, asígnele el nombre `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="cde34-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="cde34-359">En la pestaña **General** , especifique la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="cde34-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="cde34-360">**Servidor:** escriba el **Nombre de host de FTP** que ha copiado del panel.</span><span class="sxs-lookup"><span data-stu-id="cde34-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="cde34-361">**Puerto:** (déjelo en blanco, puesto que se trata de una transferencia pasiva y el servidor determinará el puerto que se utilizará).</span><span class="sxs-lookup"><span data-stu-id="cde34-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="cde34-362">**Protocolo:** FTP - Protocolo de Transferencia de Archivos</span><span class="sxs-lookup"><span data-stu-id="cde34-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="cde34-363">**Cifrado:** Use plain FTP (Usar FTP sin formato)</span><span class="sxs-lookup"><span data-stu-id="cde34-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="cde34-364">**Modo de acceso:** Normal</span><span class="sxs-lookup"><span data-stu-id="cde34-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="cde34-365">**Usuario:** introduzca el usuario de implementación / FTP que haya copiado del panel.</span><span class="sxs-lookup"><span data-stu-id="cde34-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="cde34-366">Se trata del nombre de usuario FTP completo, que tiene la forma *nombredeaplicaciónweb\nombredeusuario*.</span><span class="sxs-lookup"><span data-stu-id="cde34-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="cde34-367">**Contraseña:** escriba la contraseña que haya especificado al configurar las credenciales de implementación.</span><span class="sxs-lookup"><span data-stu-id="cde34-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="cde34-368">En la pestaña **Opciones de Transferencia**, elija **Pasivo**.</span><span class="sxs-lookup"><span data-stu-id="cde34-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="cde34-369">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-369">Click **Connect**.</span></span> <span data-ttu-id="cde34-370">Si la configuración es correcta, la consola de FileZilla mostrará el mensaje `Status: Connected` y emitirá un comando `LIST` para mostrar el contenido del directorio.</span><span class="sxs-lookup"><span data-stu-id="cde34-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="cde34-371">En el panel del sitio **Local** , elija el directorio de origen en el que reside el archivo JSPHello.war; la ruta será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cde34-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="cde34-372">En el panel del sitio **Remote** (Remoto), elija la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="cde34-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="cde34-373">El archivo WAR se implementará en el directorio `webapps` , en la raíz de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cde34-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="cde34-374">Vaya a `/site/wwwroot`, haga clic con el botón derecho en `wwwroot` y elija **Crear directorio**.</span><span class="sxs-lookup"><span data-stu-id="cde34-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="cde34-375">Asigne al directorio el nombre `webapps` y acceda a él.</span><span class="sxs-lookup"><span data-stu-id="cde34-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="cde34-376">Transfiera JSPHello.war a `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cde34-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cde34-377">Elija JSPHello.war en la lista de archivos **Local**, haga clic con el botón derecho en él y elija **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="cde34-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="cde34-378">Deberá mostrarse en `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cde34-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="cde34-379">Después de copiar JSPHello.war en el directorio de aplicaciones web, el servidor de Tomcat desempaquetará automáticamente (descomprimirá) los archivos en el archivo WAR.</span><span class="sxs-lookup"><span data-stu-id="cde34-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="cde34-380">Aunque el servidor de Tomcat comienza a desempaquetar casi inmediatamente, puede pasar mucho tiempo (posiblemente horas) para que los archivos aparezcan en el cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="cde34-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="cde34-381">Ejecución de la aplicación Hello World en la aplicación web</span><span class="sxs-lookup"><span data-stu-id="cde34-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="cde34-382">Una vez que cargue el archivo WAR y verifique que el servidor de Tomcat ha creado un directorio `JSPHello` desempaquetado, vaya a `http://webdemowebapp.azurewebsites.net/JSPHello` para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cde34-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="cde34-383">**Nota:** Si hace clic en **Examinar** desde el portal clásico, es posible que se muestre la página web predeterminada, en la que se indica que la aplicación web de Java se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="cde34-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="cde34-384">Tendrá que actualizar la página web para poder ver el resultado de la aplicación en lugar de la página web predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cde34-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="cde34-385">Cuando se ejecuta la aplicación, debería mostrarse una página web con el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="cde34-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="cde34-386">Limpieza de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="cde34-386">Clean up Azure resources</span></span>
<span data-ttu-id="cde34-387">Este procedimiento crea una aplicación web de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cde34-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="cde34-388">Se le facturará por el recurso durante toda su existencia.</span><span class="sxs-lookup"><span data-stu-id="cde34-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="cde34-389">A menos que vaya a continuar usando la aplicación web para propósitos de pruebas o desarrollo, debería plantearse si desea detenerla o eliminarla.</span><span class="sxs-lookup"><span data-stu-id="cde34-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="cde34-390">Una aplicación web detenida generará un gasto pequeño, pero podrá volver a iniciarla en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="cde34-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="cde34-391">Al eliminar una aplicación web, se borran todos los datos que se hayan cargado en ella.</span><span class="sxs-lookup"><span data-stu-id="cde34-391">Deleting a web app erases all data you have uploaded to it.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
