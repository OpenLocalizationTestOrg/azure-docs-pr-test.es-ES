---
title: "aaaCreate una aplicación Web en el servicio de aplicaciones de Azure con hello Azure SDK para Java"
description: "Obtenga información acerca de cómo toocreate una aplicación Web de servicio de aplicaciones de Azure mediante programación con hello Azure SDK para Java."
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
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="01819-103">Crear una aplicación Web en el servicio de aplicación de Azure con hello Azure SDK para Java</span><span class="sxs-lookup"><span data-stu-id="01819-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="01819-104">Información general</span><span class="sxs-lookup"><span data-stu-id="01819-104">Overview</span></span>
<span data-ttu-id="01819-105">Este tutorial muestra cómo toocreate un SDK de Azure para aplicaciones de Java que crea una aplicación Web en [servicio de aplicaciones de Azure][Azure App Service], a continuación, implemente un tooit de aplicación.</span><span class="sxs-lookup"><span data-stu-id="01819-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="01819-106">Consta de dos partes:</span><span class="sxs-lookup"><span data-stu-id="01819-106">It consists of two parts:</span></span>

* <span data-ttu-id="01819-107">Parte 1 explica cómo toobuild una aplicación Java crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="01819-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="01819-108">Parte 2 se muestra cómo toocreate un JSP simple "Hola mundo" aplicación y, a continuación, use un FTP cliente toodeploy código tooApp servicio.</span><span class="sxs-lookup"><span data-stu-id="01819-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01819-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="01819-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="01819-110">Instalaciones de software</span><span class="sxs-lookup"><span data-stu-id="01819-110">Software Installations</span></span>
<span data-ttu-id="01819-111">Hola AzureWebDemo código de la aplicación en este artículo se escribió con SDK de Java de Azure 0.7.0, que se puede instalar con hello [instalador de plataforma Web] [ Web Platform Installer] (WPI).</span><span class="sxs-lookup"><span data-stu-id="01819-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="01819-112">Además, compruebe que toouse hello más reciente de versión hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="01819-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="01819-113">Después de instalar el SDK de hello, actualizar las dependencias de hello en el proyecto de Eclipse ejecutando **Actualizar índice** en **repositorios de Maven**, a continuación, vuelva a agregar la versión más reciente de Hola de cada paquete en hello  **Dependencias** ventana.</span><span class="sxs-lookup"><span data-stu-id="01819-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="01819-114">Puede comprobar la versión de Hola del software instalado en Eclipse haciendo clic en **Ayuda > detalles de la instalación**; debe haber Hola al menos siguientes versiones:</span><span class="sxs-lookup"><span data-stu-id="01819-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="01819-115">Paquete para bibliotecas de Microsoft Azure para Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="01819-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="01819-116">IDE de Eclipse para desarrolladores de Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="01819-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="01819-117">Creación y configuración de recursos en la nube en Azure</span><span class="sxs-lookup"><span data-stu-id="01819-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="01819-118">Antes de comenzar este procedimiento, es necesario toohave una suscripción activa de Azure y configurar un valor predeterminado de Active Directory (AD) en Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="01819-119">Creación de un Active Directory (AD) en Azure</span><span class="sxs-lookup"><span data-stu-id="01819-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="01819-120">Si no tiene ya un Active Directory (AD) en su suscripción de Azure, inicie sesión en hello [portal de Azure clásico] [ Azure classic portal] con tu cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01819-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="01819-121">Si tiene varias suscripciones, haga clic en **suscripciones** y directorio de hello seleccione predeterminado para la suscripción de Hola que desee toouse para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="01819-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="01819-122">A continuación, haga clic en **aplicar** tooswitch toothat vista de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="01819-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="01819-123">Seleccione **Active Directory** desde el menú de Hola a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="01819-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="01819-124">Haga clic en **Nuevo > Directorio > Creación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="01819-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="01819-125">En **Agregar directorio**, elija **Crear nuevo directorio**.</span><span class="sxs-lookup"><span data-stu-id="01819-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="01819-126">En **Nombre**, escriba un nombre para el directorio.</span><span class="sxs-lookup"><span data-stu-id="01819-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="01819-127">En **Dominio**, escriba un nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="01819-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="01819-128">Se trata de un nombre de dominio básico que se incluye de forma predeterminada con el directorio; tiene forma de hello `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="01819-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="01819-129">Puede asignarle un nombre basado en el nombre del directorio de hello u otro nombre de dominio que posee.</span><span class="sxs-lookup"><span data-stu-id="01819-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="01819-130">Más adelante, puede agregar otro nombre de dominio que ya use su organización.</span><span class="sxs-lookup"><span data-stu-id="01819-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="01819-131">En **País o región**, elija la configuración regional que corresponda.</span><span class="sxs-lookup"><span data-stu-id="01819-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="01819-132">Para obtener más información sobre AD, consulte [¿Qué es un directorio de Azure AD?][What is an Azure AD directory]</span><span class="sxs-lookup"><span data-stu-id="01819-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="01819-133">Creación de un certificado de administración para Azure</span><span class="sxs-lookup"><span data-stu-id="01819-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="01819-134">Hello Azure SDK para Java utiliza tooauthenticate de certificados de administración con las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="01819-135">Se trata de usar una aplicación cliente que utiliza hello tooact de API de administración de servicios en nombre de recursos de la suscripción de hello suscripción propietario toomanage tooauthenticate los certificados X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="01819-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="01819-136">código de Hello en este procedimiento utiliza un certificado autofirmado tooauthenticate de Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="01819-137">Para este procedimiento, se necesita un certificado de toocreate y cargarlo toohello [portal de Azure clásico] [ Azure classic portal] con antelación.</span><span class="sxs-lookup"><span data-stu-id="01819-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="01819-138">Esto implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="01819-138">This involves hello following steps:</span></span>

* <span data-ttu-id="01819-139">Generar un archivo PFX que represente el certificado de cliente y guardarlo localmente.</span><span class="sxs-lookup"><span data-stu-id="01819-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="01819-140">Generar un certificado de administración (archivo .cer) del archivo PFX de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="01819-141">Cargar Hola CER archivo tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="01819-142">Convertir archivo PFX de hello en el almacén JKS, dado que Java utiliza ese tooauthenticate formato mediante certificados.</span><span class="sxs-lookup"><span data-stu-id="01819-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="01819-143">Escribir código de autenticación de la aplicación hello, que hace referencia el archivo de almacén JKS local toohello.</span><span class="sxs-lookup"><span data-stu-id="01819-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="01819-144">Al completar este procedimiento, certificado CER de hello residirá en la suscripción de Azure y certificado de almacén JKS Hola residirá en la unidad local.</span><span class="sxs-lookup"><span data-stu-id="01819-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="01819-145">Para obtener más información sobre la administración de certificados, consulte [Crear y cargar un certificado de administración para Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="01819-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="01819-146">Creación de un certificado</span><span class="sxs-lookup"><span data-stu-id="01819-146">Create a certificate</span></span>
<span data-ttu-id="01819-147">toocreate su propio certificado autofirmado, abra una consola de comandos en el sistema operativo y ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="01819-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="01819-148">**Nota:** equipo hello en el que se ejecuta este comando debe tener Hola JDK instalado.</span><span class="sxs-lookup"><span data-stu-id="01819-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="01819-149">Además, la Hola ruta de acceso toohello keytool depende de la ubicación de Hola de instalación de JDK Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="01819-150">Para obtener más información, consulte [clave y la herramienta de administración de certificados (keytool)] [ Key and Certificate Management Tool (keytool)] en documentos de hello Java en línea.</span><span class="sxs-lookup"><span data-stu-id="01819-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="01819-151">archivo .pfx de toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="01819-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="01819-152">archivo .cer de toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="01819-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="01819-153">donde:</span><span class="sxs-lookup"><span data-stu-id="01819-153">where:</span></span>

* <span data-ttu-id="01819-154">`<java-install-dir>`es el directorio de toohello de ruta de acceso de hello en el que se instaló Java.</span><span class="sxs-lookup"><span data-stu-id="01819-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="01819-155">`<keystore-id>`es el identificador de entrada del almacén de claves de hello (por ejemplo, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="01819-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="01819-156">`<cert-store-dir>`es Hola ruta de acceso toohello directorio en el que desea que los certificados de toostore (por ejemplo `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="01819-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="01819-157">`<cert-file-name>`es el nombre de Hola Hola del archivo de certificado (por ejemplo `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="01819-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="01819-158">`<password>`es la contraseña Hola elige tooprotect Hola certificado; debe ser al menos 6 caracteres.</span><span class="sxs-lookup"><span data-stu-id="01819-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="01819-159">Se puede optar por no escribir ninguna contraseña, aunque no se recomienda.</span><span class="sxs-lookup"><span data-stu-id="01819-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="01819-160">`<dname>`es Hola nombre distintivo X.500 toobe asociado con el alias y se utiliza como emisor de Hola y los campos de sujeto de certificado autofirmado Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="01819-161">Para obtener más información, consulte [Crear y cargar un certificado de administración para Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="01819-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="01819-162">Cargar certificado Hola</span><span class="sxs-lookup"><span data-stu-id="01819-162">Upload hello certificate</span></span>
<span data-ttu-id="01819-163">tooupload tooAzure de un certificado autofirmado, vaya toohello **configuración** página portal clásico de hello, haga clic en hello **certificados de administración** ficha. Haga clic en **cargar** final Hola de hello página y navegar toohello ubicación del archivo CER Hola creado.</span><span class="sxs-lookup"><span data-stu-id="01819-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="01819-164">Convertir archivo PFX de hello en el almacén JKS</span><span class="sxs-lookup"><span data-stu-id="01819-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="01819-165">Hola de línea de comandos de Windows (que se ejecuta como administrador), cd toohello directorio que contiene Hola certificados y ejecute hello siguiente comando, donde `<java-install-dir>` es el directorio de hello en el que instaló Java en el equipo:</span><span class="sxs-lookup"><span data-stu-id="01819-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="01819-166">Cuando se le solicite, escriba la contraseña del almacén de claves de destino de hello; se trata de contraseña de hello para el archivo de almacén JKS hello.</span><span class="sxs-lookup"><span data-stu-id="01819-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="01819-167">Cuando se le solicite, escriba la contraseña del almacén de claves de origen de hello; se trata de una contraseña de Hola que especificó para el archivo PFX de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="01819-168">las dos contraseñas de Hello no tiene toobe Hola igual.</span><span class="sxs-lookup"><span data-stu-id="01819-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="01819-169">Se puede optar por no escribir ninguna contraseña, aunque no se recomienda.</span><span class="sxs-lookup"><span data-stu-id="01819-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="01819-170">Compilación de una aplicación para crear aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="01819-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="01819-171">Crear Hola área de trabajo de Eclipse y proyectos de Maven</span><span class="sxs-lookup"><span data-stu-id="01819-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="01819-172">En esta sección se creará un área de trabajo y un proyecto de Maven para la aplicación de creación de aplicaciones de web hello, denominado AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="01819-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="01819-173">Cree un nuevo proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="01819-173">Create a new Maven project.</span></span> <span data-ttu-id="01819-174">Haga clic en **File (Archivo) > New (Nuevo) > Maven Project (Proyecto de Maven)**.</span><span class="sxs-lookup"><span data-stu-id="01819-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="01819-175">En **New Maven Project** (Nuevo proyecto de Maven), elija **Create a simple project** (Crear proyecto sencillo) y, a continuación, elija **Use default workspace location** (Usar ubicación de espacio de trabajo predeterminada).</span><span class="sxs-lookup"><span data-stu-id="01819-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="01819-176">En la segunda página de Hola de **Maven proyecto**, especifique Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="01819-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="01819-177">Group ID (Identificador del grupo): `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="01819-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="01819-178">Artifact ID (Identificador de artefacto): AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="01819-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="01819-179">Version (Versión): 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="01819-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="01819-180">Packaging (Empaquetado): jar</span><span class="sxs-lookup"><span data-stu-id="01819-180">Packaging: jar</span></span>
   * <span data-ttu-id="01819-181">Name (Nombre): AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="01819-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="01819-182">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="01819-182">Click **Finish**.</span></span>
3. <span data-ttu-id="01819-183">Abra el archivo de pom.xml del nuevo proyecto de hello en el Explorador de proyectos.</span><span class="sxs-lookup"><span data-stu-id="01819-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="01819-184">Seleccione hello **dependencias** ficha. Como se trata de un nuevo proyecto, todavía no se muestra ningún paquete.</span><span class="sxs-lookup"><span data-stu-id="01819-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="01819-185">Ver los repositorios de Maven Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="01819-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="01819-186">**Haga clic en Window (Ventana) &gt; Show View (Mostrar vista) &gt; Other (Otro) &gt; Maven &gt; Maven Repositories (Repositorios de Maven)** y luego en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="01819-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="01819-187">Hola **Maven repositorios** vista aparecerá en parte inferior de Hola de hello IDE.</span><span class="sxs-lookup"><span data-stu-id="01819-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="01819-188">Abra **repositorios globales**, contextual hello **central** repositorio y seleccione **volver a generar índice**.</span><span class="sxs-lookup"><span data-stu-id="01819-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="01819-189">Este paso puede tardar varios minutos, según la velocidad de saludo de la conexión.</span><span class="sxs-lookup"><span data-stu-id="01819-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="01819-190">Cuando se vuelve a generar el índice de hello, debería ver paquetes de Microsoft Azure de hello en hello **central** repositorio de Maven.</span><span class="sxs-lookup"><span data-stu-id="01819-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="01819-191">En **Dependencies** (Dependencias), haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="01819-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="01819-192">En **Enter Group ID...** (Especificar identificador de grupo), escriba `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="01819-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="01819-193">Seleccionar paquetes de saludo para administración de la base y la administración de aplicaciones Web de servicio de aplicación:</span><span class="sxs-lookup"><span data-stu-id="01819-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="01819-194">**Nota:** si va a actualizar las dependencias de hello después de una nueva versión de lanzamiento, necesita toore-agregar cada una de las dependencias de hello en esta lista.</span><span class="sxs-lookup"><span data-stu-id="01819-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="01819-195">Tras hacer clic en **agregar** y seleccione cada dependencia, ésta aparece con el nuevo número de versión Hola Hola **dependencias** lista.</span><span class="sxs-lookup"><span data-stu-id="01819-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="01819-196">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="01819-196">Click **OK**.</span></span> <span data-ttu-id="01819-197">Hola paquetes de Azure, a continuación, aparecen en hello **dependencias** lista.</span><span class="sxs-lookup"><span data-stu-id="01819-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="01819-198">Escribir código Java tooCreate una aplicación Web que realiza la llamada hello Azure SDK</span><span class="sxs-lookup"><span data-stu-id="01819-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="01819-199">A continuación, escribir código de hello que llama a las API de hello Azure SDK para hello de Java toocreate aplicación de servicio de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="01819-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="01819-200">Crear un código de punto de entrada principal de Java clase toocontain Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="01819-201">En el Explorador de proyectos, haga doble clic en el nodo del proyecto de Hola y seleccione **nuevo > clase**.</span><span class="sxs-lookup"><span data-stu-id="01819-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="01819-202">En **nueva clase de Java**, el nombre de clase hello `WebCreator` y comprobar hello **principal de void estático público** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="01819-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="01819-203">selecciones de Hello deberían aparecer como sigue:</span><span class="sxs-lookup"><span data-stu-id="01819-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="01819-204">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="01819-204">Click **Finish**.</span></span> <span data-ttu-id="01819-205">archivo de Hello WebCreator.java aparece en el Explorador de proyectos.</span><span class="sxs-lookup"><span data-stu-id="01819-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="01819-206">Al llamar a hello Azure API tooCreate una aplicación de servicio de aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="01819-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="01819-207">Adición de las importaciones necesarias</span><span class="sxs-lookup"><span data-stu-id="01819-207">Add necessary imports</span></span>
<span data-ttu-id="01819-208">En WebCreator.java, agregue Hola siguiendo las importaciones; estas importaciones proporcionan acceso tooclasses en hello las bibliotecas de administración para utilizar las API de Azure:</span><span class="sxs-lookup"><span data-stu-id="01819-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="01819-209">Definir la clase de punto de entrada principal de hello</span><span class="sxs-lookup"><span data-stu-id="01819-209">Define hello main entry point class</span></span>
<span data-ttu-id="01819-210">Porque Hola de hello AzureWebDemo aplicación sirve toocreate una aplicación de servicio de aplicaciones Web, name clase principal de Hola para esta aplicación `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="01819-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="01819-211">Esta clase proporciona código de punto de entrada principal de Hola que llama la aplicación web de hello API de administración de servicios de Azure toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="01819-212">Agregar Hola siguiendo las definiciones de parámetro para la aplicación web de hello y espacio Web.</span><span class="sxs-lookup"><span data-stu-id="01819-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="01819-213">Necesitará tooprovide su propia información de identificador y el certificado de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="01819-214">donde:</span><span class="sxs-lookup"><span data-stu-id="01819-214">where:</span></span>

* <span data-ttu-id="01819-215">`<subscription-id>`es el Id. de suscripción de Azure de hello en el que desea que el recurso de Hola de toocreate.</span><span class="sxs-lookup"><span data-stu-id="01819-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="01819-216">`<certificate-store-path>`es la ruta de acceso y nombre de archivo toohello almacén JKS archivo hello en el directorio de almacén de certificados local.</span><span class="sxs-lookup"><span data-stu-id="01819-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="01819-217">Por ejemplo, `C:/Certificates/CertificateName.jks` para Linux y `C:\Certificates\CertificateName.jks` para Windows.</span><span class="sxs-lookup"><span data-stu-id="01819-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="01819-218">`<certificate-password>`es la contraseña de Hola que especificó cuando creó el certificado del almacén JKS.</span><span class="sxs-lookup"><span data-stu-id="01819-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="01819-219">`webAppName`puede ser cualquier nombre que elija; Este procedimiento utiliza el nombre de hello `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="01819-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="01819-220">nombre de dominio completo de Hello es hello `webAppName` con hello `domainName` anexado, por lo que en este caso dominio completo de hello es `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="01819-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="01819-221">`domainName` debe especificarse del modo indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="01819-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="01819-222">`webSpaceName`debe ser uno de los valores de hello definidos en hello [WebSpaceNames] [ WebSpaceNames] clase.</span><span class="sxs-lookup"><span data-stu-id="01819-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="01819-223">`appServicePlanName` debe especificarse del modo indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="01819-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="01819-224">**Nota:** cada vez que se ejecuta esta aplicación, necesita toochange Hola valo `webAppName` y `appServicePlanName` (o eliminar la aplicación web de hello en hello Portal de Azure) antes de ejecutar de nuevo la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="01819-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="01819-225">En caso contrario, se producirá un error la ejecución porque hello mismo recurso ya existe en Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="01819-226">Definir el método de creación de hello web</span><span class="sxs-lookup"><span data-stu-id="01819-226">Define hello web creation method</span></span>
<span data-ttu-id="01819-227">A continuación, defina una aplicación web de método toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="01819-228">Este método, `createWebApp`, especifica los parámetros de Hola de hello web app y espacio Web Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="01819-229">También crea y configura el cliente de administración de aplicaciones Web de servicio de aplicación hello, que se define por hello [WebSiteManagementClient] [ WebSiteManagementClient] objeto.</span><span class="sxs-lookup"><span data-stu-id="01819-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="01819-230">cliente de administración de Hello es clave toocreating las aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="01819-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="01819-231">Proporciona servicios web RESTful que permiten a las aplicaciones toomanage aplicaciones web (realizar operaciones como crear, update y delete) mediante una llamada a la API de administración de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
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
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="01819-232">código de Hello dará como resultado de estado HTTP Hola de respuesta de Hola que indica éxito o error y si se realiza correctamente, dará como resultado el nombre de Hola de hello creado la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="01819-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="01819-233">Definir el método main() de Hola</span><span class="sxs-lookup"><span data-stu-id="01819-233">Define hello main() method</span></span>
<span data-ttu-id="01819-234">Proporcionar código del método main() Hola esa aplicación web de llamadas createWebApp() toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="01819-235">Por último, efectúe una llamada a `createWebApp` desde `main`:</span><span class="sxs-lookup"><span data-stu-id="01819-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="01819-236">Ejecutar la aplicación hello y comprobar la creación de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="01819-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="01819-237">tooverify que se ejecuta la aplicación, haga clic en **ejecutar > ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="01819-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="01819-238">Cuando complete la ejecución de aplicación hello, debería ver Hola después de salida en la consola de Eclipse hello:</span><span class="sxs-lookup"><span data-stu-id="01819-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="01819-239">Inicie sesión en el portal de Azure clásico de Hola y haga clic en **aplicaciones Web**.</span><span class="sxs-lookup"><span data-stu-id="01819-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="01819-240">aplicación web nueva de Hello debe aparecer en la lista de aplicaciones Web de hello dentro de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="01819-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="01819-241">Implementar una aplicación Web de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="01819-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="01819-242">Después de que han ejecutado AzureWebDemo y creó Hola nueva aplicación web, inicie sesión en el portal clásico de hello, haga clic en **aplicaciones Web**y seleccione **WebDemoWebApp** en hello **aplicaciones Web** lista.</span><span class="sxs-lookup"><span data-stu-id="01819-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="01819-243">En la página del panel de la aplicación de hello web, haga clic en **examinar** (o haga clic en la dirección URL de hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="01819-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="01819-244">Verá una página de marcador de posición en blanco, porque no hay contenido ha sido publicado toohello web app aún.</span><span class="sxs-lookup"><span data-stu-id="01819-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="01819-245">A continuación creará una aplicación "Hello World" e implementar toohello web app.</span><span class="sxs-lookup"><span data-stu-id="01819-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="01819-246">Creación de una aplicación Hello World en JSP</span><span class="sxs-lookup"><span data-stu-id="01819-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="01819-247">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="01819-247">Create hello application</span></span>
<span data-ttu-id="01819-248">En toodemonstrate orden cómo Hola toodeploy web toohello aplicación, siga el procedimiento muestra cómo toocreate una sencilla aplicación de Java de "Hello World" y la carga toohello aplicación Web de aplicación de servicio que creó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01819-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="01819-249">Haga clic en **File (Archivo) > New (Nuevo) > Dynamic Web Project (Proyecto web dinámico)**.</span><span class="sxs-lookup"><span data-stu-id="01819-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="01819-250">Asígnele el nombre `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="01819-250">Name it `JSPHello`.</span></span> <span data-ttu-id="01819-251">No es necesario toochange ninguna otra configuración de este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01819-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="01819-252">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="01819-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="01819-253">En el Explorador de proyectos, expanda hello **JSPHello** proyecto de equipo y haga clic en **WebContent**, a continuación, haga clic en **nuevo > archivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="01819-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="01819-254">En el cuadro de diálogo de nuevo archivo JSP hello, nombre hello nuevo archivo `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="01819-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="01819-255">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="01819-255">Click **Next**.</span></span>
3. <span data-ttu-id="01819-256">Hola **Select JSP Template** cuadro de diálogo, seleccione **New JSP File (html)** y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="01819-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="01819-257">En el archivo index.jsp agregar Hola después el código de hello `<head>` y `<body>` etiquetar secciones:</span><span class="sxs-lookup"><span data-stu-id="01819-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="01819-258">Ejecutar la aplicación hello World Hello en localhost</span><span class="sxs-lookup"><span data-stu-id="01819-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="01819-259">Antes de ejecutar esta aplicación, necesita tooconfigure algunas propiedades.</span><span class="sxs-lookup"><span data-stu-id="01819-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="01819-260">Menú contextual hello **JSPHello** de proyecto y seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="01819-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="01819-261">Hola **propiedades** diálogo: seleccione **Java Build Path**, seleccione hello **ordenar y exportar** ficha, comprobación de **JRE biblioteca del sistema**, a continuación, haga clic en **Una** toomove se toohello superior de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="01819-262">También en hello **propiedades** diálogo: seleccione **tiempos de ejecución de destino** y haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="01819-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="01819-263">Hola **nuevo entorno de tiempo de ejecución de servidor** cuadro de diálogo, seleccione un servidor como **Apache Tomcat v7.0** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="01819-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="01819-264">Hola **servidor de Tomcat** cuadro de diálogo, establezca **nombre** demasiado`Apache Tomcat v7.0`y establezca **directorio de instalación de Tomcat** directorio toohello en el que instaló la versión de Hola de Servidor de Tomcat que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="01819-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="01819-265">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="01819-265">Click **Finish**.</span></span>
5. <span data-ttu-id="01819-266">A continuación, devolver toohello **tiempos de ejecución de destino** página de hello **propiedades** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01819-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="01819-267">Elija **Apache Tomcat v7.0** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="01819-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="01819-268">Hola Eclipse **ejecutar** menú, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="01819-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="01819-269">Hola **ejecución** cuadro de diálogo, seleccione **ejecutar en el servidor**.</span><span class="sxs-lookup"><span data-stu-id="01819-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="01819-270">Hola **ejecutar en el servidor** cuadro de diálogo, seleccione **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="01819-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="01819-271">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="01819-271">Click **Finish**.</span></span>
7. <span data-ttu-id="01819-272">Hola cuando ejecuta la aplicación, debería ver Hola **JSPHello** página aparecen en una ventana de localhost en Eclipse (`http://localhost:8080/JSPHello/`), mostrar Hola siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="01819-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="01819-273">Exportar aplicación hello como una guerra</span><span class="sxs-lookup"><span data-stu-id="01819-273">Export hello application as a WAR</span></span>
<span data-ttu-id="01819-274">Exportar archivos de proyecto de hello web como un archivo web (WAR) para que pueda implementar toohello web app.</span><span class="sxs-lookup"><span data-stu-id="01819-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="01819-275">Hello siguientes archivos de proyecto web residen en hello WebContent carpeta:</span><span class="sxs-lookup"><span data-stu-id="01819-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="01819-276">Haga clic en carpeta de hello WebContent y seleccione **exportar**.</span><span class="sxs-lookup"><span data-stu-id="01819-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="01819-277">Hola **Exportar seleccione** cuadro de diálogo, haga clic en **Web > WAR** de archivos, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="01819-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="01819-278">Hola **exportar WAR** cuadro de diálogo, seleccione el directorio de src de hello en el proyecto actual de hello e incluir nombre de Hola de archivo WAR de hello final Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="01819-279">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="01819-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="01819-280">Para obtener más información sobre cómo implementar archivos WAR, consulte [agregar una tooAzure de aplicación de Java aplicación del servicio de aplicaciones Web](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="01819-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="01819-281">Implementar Hola Hola mundo aplicación mediante FTP</span><span class="sxs-lookup"><span data-stu-id="01819-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="01819-282">Seleccione una aplicación de terceros FTP cliente toopublish Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="01819-283">Este procedimiento describe dos opciones: consola de Kudu Hola integrada en Azure; y FileZilla, una herramienta muy usada con una interfaz de usuario adecuada, gráfica.</span><span class="sxs-lookup"><span data-stu-id="01819-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="01819-284">**Nota:** Hola Kit de herramientas de Azure para Eclipse es compatible con cuentas de implementación de toostorage y servicios en la nube, pero no admite actualmente las aplicaciones de tooweb de implementación.</span><span class="sxs-lookup"><span data-stu-id="01819-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="01819-285">Puede implementar toostorage cuentas y servicios mediante un proyecto de implementación de Azure como se describe en la nube [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), pero no a las aplicaciones tooweb.</span><span class="sxs-lookup"><span data-stu-id="01819-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="01819-286">Utilizar otros métodos, como FTP o GitHub tootransfer archivos tooyour aplicación web.</span><span class="sxs-lookup"><span data-stu-id="01819-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="01819-287">**Nota:** no se recomienda usar FTP desde la línea de comandos de Windows hello (Hola de línea de comandos FTP.EXE utilidad que se incluye con Windows).</span><span class="sxs-lookup"><span data-stu-id="01819-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="01819-288">Los clientes FTP que utilicen FTP activo, por ejemplo, FTP.EXE, a menudo no toowork a través de firewalls.</span><span class="sxs-lookup"><span data-stu-id="01819-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="01819-289">FTP activo especifica una dirección interna basado en LAN, servidor FTP toowhich probablemente se producirá un error tooconnect.</span><span class="sxs-lookup"><span data-stu-id="01819-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="01819-290">Para obtener más información sobre la aplicación del servicio de aplicaciones web de implementación tooan mediante FTP, vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="01819-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="01819-291">Implementación mediante una utilidad FTP</span><span class="sxs-lookup"><span data-stu-id="01819-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="01819-292">Configurar credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="01819-292">Set up deployment credentials</span></span>
<span data-ttu-id="01819-293">Asegúrese de que ha ejecutado hello **AzureWebDemo** aplicación toocreate una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="01819-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="01819-294">Transferirá ubicación toothis de archivos.</span><span class="sxs-lookup"><span data-stu-id="01819-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="01819-295">Inicie sesión en el portal clásico de Hola y haga clic en **aplicaciones Web**.</span><span class="sxs-lookup"><span data-stu-id="01819-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="01819-296">Asegúrese de que **WebDemoWebApp** aparece en la lista de Hola de aplicaciones web y asegúrese de que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="01819-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="01819-297">Haga clic en **WebDemoWebApp** tooopen su **panel** página.</span><span class="sxs-lookup"><span data-stu-id="01819-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="01819-298">En hello **panel** página, en **vista rápida**, haga clic en **configurar las credenciales de implementación** (si ya tiene las credenciales de implementación, éste lee  **Restablecer las credenciales de implementación**).</span><span class="sxs-lookup"><span data-stu-id="01819-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="01819-299">Credenciales de implementación asociadas con una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01819-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="01819-300">Deberá toospecify un nombre de usuario y la contraseña que se puede usar toodeploy mediante Git y FTP.</span><span class="sxs-lookup"><span data-stu-id="01819-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="01819-301">Puede usar estas aplicaciones web de credenciales toodeploy tooany en todas las suscripciones de Azure asociadas a su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01819-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="01819-302">Proporcione las credenciales de implementación de Git y FTP en el cuadro de diálogo de hello y el nombre de usuario de registro hello y una contraseña para un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="01819-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="01819-303">Obtención de la información de conexión para FTP</span><span class="sxs-lookup"><span data-stu-id="01819-303">Get FTP connection information</span></span>
<span data-ttu-id="01819-304">toouse FTP toodeploy aplicación archivos toohello que acaba de crear aplicación web, necesitará información de conexión de tooobtain.</span><span class="sxs-lookup"><span data-stu-id="01819-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="01819-305">Hay dos maneras de obtener información de conexión de tooobtain.</span><span class="sxs-lookup"><span data-stu-id="01819-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="01819-306">Una manera es la aplicación web de toovisit hello **panel** página; hello otra manera es perfil de publicación de la aplicación web de toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="01819-307">perfil de publicación de Hello es un archivo XML que proporciona información como credenciales de inicio de sesión y el nombre de host FTP para las aplicaciones web en el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="01819-308">Puede usar esta aplicación toodeploy tooany web de nombre de usuario y contraseña en todas las suscripciones asociadas con hello cuenta de Azure, no solo este uno.</span><span class="sxs-lookup"><span data-stu-id="01819-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="01819-309">información de conexión de tooobtain FTP de hoja de la aplicación web Hola Hola [Portal de Azure][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="01819-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="01819-310">En **Essentials**, busque y copie hello **nombre de host FTP**.</span><span class="sxs-lookup"><span data-stu-id="01819-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="01819-311">Esto es un URI similar demasiado`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="01819-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="01819-312">En **Essentials**, busque y copie **FTP/Nombre de usuario de implementación**.</span><span class="sxs-lookup"><span data-stu-id="01819-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="01819-313">Esto provocará que el formulario de hello *webappname\deployment-username*; por ejemplo `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="01819-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="01819-314">perfil de publicación de información de conexión de FTP tooobtain de hello:</span><span class="sxs-lookup"><span data-stu-id="01819-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="01819-315">En la hoja de la aplicación de hello web, haga clic en **Get perfil de publicación**.</span><span class="sxs-lookup"><span data-stu-id="01819-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="01819-316">Se descargará una unidad local de .publishsettings archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="01819-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="01819-317">Abra el archivo .publishsettings de hello en un editor XML o editor de texto y busque hello `<publishProfile>` que contiene el elemento `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="01819-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="01819-318">Debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="01819-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="01819-319">Tenga en cuenta esa aplicación de web hello `publishProfile` configuración asignar configuración de administrador del sitio FileZilla toohello como sigue:</span><span class="sxs-lookup"><span data-stu-id="01819-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="01819-320">`publishUrl`se Hola igual **nombre de host FTP**, Hola valor establecido en **Host**.</span><span class="sxs-lookup"><span data-stu-id="01819-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="01819-321">`publishMethod="FTP"`significa que se establece **protocolo** demasiado**FTP: protocolo de transferencia de archivos**, y **cifrado** demasiado**usar FTP sin formato**.</span><span class="sxs-lookup"><span data-stu-id="01819-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="01819-322">`userName`y `userPWD` son claves para hello valores reales de nombre de usuario y la contraseña que especificó al restablecer credenciales de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="01819-323">`userName`se Hola igual **implementación / FTP usuario**.</span><span class="sxs-lookup"><span data-stu-id="01819-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="01819-324">Se asignan demasiado**usuario** y **contraseña** en FileZilla.</span><span class="sxs-lookup"><span data-stu-id="01819-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="01819-325">`ftpPassiveMode="True"`significa que ese sitio Hola FTP utiliza a transferencia FTP pasivo; Seleccione **pasivo** en hello **configuración de transferencia** ficha.</span><span class="sxs-lookup"><span data-stu-id="01819-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="01819-326">Configurar la aplicación Web de hello toohost una aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="01819-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="01819-327">Antes de publicar la aplicación hello, tendrá que toochange algunos valores de configuración para que hello aplicación web puede hospedar una aplicación Java.</span><span class="sxs-lookup"><span data-stu-id="01819-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="01819-328">En el portal clásico de hello, vaya toohello web app **panel** página y haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="01819-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="01819-329">En hello **configurar** página, especifique Hola después de la configuración.</span><span class="sxs-lookup"><span data-stu-id="01819-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="01819-330">En **versión de Java** Hola predeterminado es **desactivar**; seleccione versión de Java de hello destine su aplicación; por ejemplo 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="01819-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="01819-331">Después de hacer esto, también Asegúrese de que **contenedor Web** se establece la versión de tooa de servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="01819-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="01819-332">En **documentos predeterminados**, agregue index.jsp y moverlo hacia arriba de la parte superior de toohello de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="01819-333">(archivo de saludo predeterminado para las aplicaciones web es hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="01819-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="01819-334">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01819-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="01819-335">Publicación de la aplicación mediante Kudu</span><span class="sxs-lookup"><span data-stu-id="01819-335">Publish your application using Kudu</span></span>
<span data-ttu-id="01819-336">Aplicación de una manera toopublish hello es hello toouse que kudu depurar consola integrada en Azure.</span><span class="sxs-lookup"><span data-stu-id="01819-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="01819-337">Kudu se conoce toobe estable y coherente con la aplicación del servicio de aplicaciones Web y el servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="01819-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="01819-338">Tener acceso a la consola de hello para la aplicación web de hello examinando la dirección URL de tooa de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="01819-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="01819-339">Para este procedimiento, consola de hello Kudu se encuentra en hello después de la dirección URL; Busque la ubicación de toothis:</span><span class="sxs-lookup"><span data-stu-id="01819-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="01819-340">En el menú superior de hello, seleccione **consola Depurar > CMD**.</span><span class="sxs-lookup"><span data-stu-id="01819-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="01819-341">En la línea de comandos de consola de hello, navegue demasiado`/site/wwwroot` (o haga clic en `site`, a continuación, `wwwroot` en la vista de directorio de hello al principio de Hola de página de hello):</span><span class="sxs-lookup"><span data-stu-id="01819-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="01819-342">Después de especificar un valor en **Versión de Java**, el servidor de Tomcat debe crear un directorio de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="01819-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="01819-343">En la línea de comandos de consola de hello, desplácese toohello directorio de aplicaciones Web:</span><span class="sxs-lookup"><span data-stu-id="01819-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="01819-344">Arrastre JSPHello.war de `<project-path>/JSPHello/src/` y colóquelo en la vista de directorio de hello Kudu en `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="01819-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="01819-345">No lo arrastre toohello "Arrastre aquí tooupload y zip" área, porque descomprímalo Tomcat.</span><span class="sxs-lookup"><span data-stu-id="01819-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="01819-346">En JSPHello.war primera aparece en el área de directorio de Hola por sí solo:</span><span class="sxs-lookup"><span data-stu-id="01819-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="01819-347">En poco tiempo (probablemente menos de 5 minutos) servidor de Tomcat se descomprima el archivo WAR de hello en un directorio JSPHello desempaquetado.</span><span class="sxs-lookup"><span data-stu-id="01819-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="01819-348">Haga clic en hello raíz directory toosee si se ha descomprimido index.jsp y se copiarán allí.</span><span class="sxs-lookup"><span data-stu-id="01819-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="01819-349">Si es así, vaya toosee de directorio de aplicaciones Web toohello atrás si Hola desempaqueta JSPHello se ha creado el directorio.</span><span class="sxs-lookup"><span data-stu-id="01819-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="01819-350">Si no ve estos elementos, espere y repita el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="01819-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="01819-351">Publicación de la aplicación mediante FileZilla (opcional)</span><span class="sxs-lookup"><span data-stu-id="01819-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="01819-352">Otra herramienta que puede usar la aplicación de hello toopublish es FileZilla, un cliente FTP de otros fabricantes popular con una interfaz de usuario adecuada, gráfico.</span><span class="sxs-lookup"><span data-stu-id="01819-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="01819-353">Puede descargar e instalar FileZilla desde [http://filezilla-project.org/](http://filezilla-project.org/) en caso de que no lo tenga.</span><span class="sxs-lookup"><span data-stu-id="01819-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="01819-354">Para obtener más información sobre el uso de cliente hello, vea hello [FileZilla documentación](https://wiki.filezilla-project.org/Documentation) y esta entrada de blog en [los clientes FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="01819-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="01819-355">En FileZilla, haga clic en **Archivo > Gestor de sitios**.</span><span class="sxs-lookup"><span data-stu-id="01819-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="01819-356">Hola **Site Manager** cuadro de diálogo, haga clic en **nuevo sitio**.</span><span class="sxs-lookup"><span data-stu-id="01819-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="01819-357">Aparecerá un nuevo sitio FTP en blanco en **Seleccionar entrada** preguntar tooprovide un nombre.</span><span class="sxs-lookup"><span data-stu-id="01819-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="01819-358">Para este procedimiento, asígnele el nombre `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="01819-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="01819-359">En hello **General** ficha, especifique Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="01819-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="01819-360">**Host:** ENTRAR hello **nombre de Host FTP** que copió desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="01819-361">**Puerto:** (dejarlo en blanco, tal y como se trata de una transferencia de pasivo y servidor hello determinará Hola puerto toouse.)</span><span class="sxs-lookup"><span data-stu-id="01819-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="01819-362">**Protocolo:** FTP - Protocolo de Transferencia de Archivos</span><span class="sxs-lookup"><span data-stu-id="01819-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="01819-363">**Cifrado:** Use plain FTP (Usar FTP sin formato)</span><span class="sxs-lookup"><span data-stu-id="01819-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="01819-364">**Modo de acceso:** Normal</span><span class="sxs-lookup"><span data-stu-id="01819-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="01819-365">**Usuario:** ENTRAR Hola implementación / FTP de usuario que ha copiado en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="01819-366">Se trata de hello nombre de usuario FTP completo, que tiene formato de hello *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="01819-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="01819-367">**Contraseña:** escriba la contraseña de Hola que especificó al configurar las credenciales de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="01819-368">En hello **configuración de transferencia** ficha, seleccione **pasivo**.</span><span class="sxs-lookup"><span data-stu-id="01819-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="01819-369">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="01819-369">Click **Connect**.</span></span> <span data-ttu-id="01819-370">Si es correcta, consola del FileZilla se mostrará un `Status: Connected` mensaje y emitir un `LIST` comando contenido del directorio toolist Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="01819-371">Hola **Local** el panel de sitio, directorio de origen de hello seleccione en qué archivo de JSPHello.war hello reside; ruta de acceso de hello será similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="01819-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="01819-372">Hola **remoto** panel sitio, la carpeta de destino de hello select.</span><span class="sxs-lookup"><span data-stu-id="01819-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="01819-373">Implementará Hola WAR archivo toohello `webapps` directorio en la raíz de la aplicación hello web.</span><span class="sxs-lookup"><span data-stu-id="01819-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="01819-374">Navegue demasiado`/site/wwwroot`, haga doble clic en `wwwroot`y seleccione **crear directorio**.</span><span class="sxs-lookup"><span data-stu-id="01819-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="01819-375">Directorio de nombres de hello `webapps` y escriba ese directorio.</span><span class="sxs-lookup"><span data-stu-id="01819-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="01819-376">Transferir JSPHello.war demasiado`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="01819-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="01819-377">Seleccione JSPHello.war en hello **Local** lista de archivos, haga doble clic en él y seleccione **cargar**.</span><span class="sxs-lookup"><span data-stu-id="01819-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="01819-378">Deberá mostrarse en `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="01819-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="01819-379">Una vez copiado el directorio de aplicaciones Web de JSPHello.war toohello, automáticamente se desempaquetar el servidor de Tomcat (Descomprimir) Hola archivos en archivo WAR de hello.</span><span class="sxs-lookup"><span data-stu-id="01819-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="01819-380">Aunque el servidor de Tomcat comienza a desempaquetar casi de inmediato, es posible que tarde mucho tiempo (posiblemente horas) para hello tooappear de archivos de cliente de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="01819-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="01819-381">Ejecutar aplicación hello Hello World en hello aplicación Web</span><span class="sxs-lookup"><span data-stu-id="01819-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="01819-382">Una vez que haya cargado el archivo WAR de hello y comprobar que el servidor de Tomcat ha creado un desempaquetados `JSPHello` directory, examinar demasiado`http://webdemowebapp.azurewebsites.net/JSPHello` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="01819-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="01819-383">**Nota:** si hace clic en **examinar** desde portal clásico de hello, podría obtener página Web predeterminada de hello, que dice "esta aplicación web de Java según se creó correctamente."</span><span class="sxs-lookup"><span data-stu-id="01819-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="01819-384">Podría tener página Web de hello toorefresh en orden tooview Hola salida de la aplicación en lugar de la página Web predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="01819-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="01819-385">Cuando se ejecuta la aplicación hello, verá una página web con hello después de salida:</span><span class="sxs-lookup"><span data-stu-id="01819-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="01819-386">Limpieza de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="01819-386">Clean up Azure resources</span></span>
<span data-ttu-id="01819-387">Este procedimiento crea una aplicación web de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="01819-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="01819-388">Se le facturará para el recurso de hello mientras existe.</span><span class="sxs-lookup"><span data-stu-id="01819-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="01819-389">A menos que piense toocontinue con hello web app para pruebas o desarrollo, debería considerar detener o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="01819-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="01819-390">Una aplicación web detenida generará un gasto pequeño, pero podrá volver a iniciarla en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="01819-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="01819-391">Eliminar una aplicación web, borra todos los datos que se ha cargado tooit.</span><span class="sxs-lookup"><span data-stu-id="01819-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

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
