---
title: "Instalación del kit de herramientas de Azure para Eclipse | Microsoft Docs"
description: "Descubra cómo instalar el kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="2c8fe-103">Instalación del Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="2c8fe-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="2c8fe-104">El kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones de Azure fácilmente con el entorno de desarrollo de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="2c8fe-105">El kit de herramientas de Azure para Eclipse es un proyecto de código abierto.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="2c8fe-106">El código fuente está disponible bajo la licencia MIT en <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="2c8fe-107">En los pasos siguientes se muestra cómo instalar el Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="2c8fe-108">Para instalar el Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="2c8fe-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="2c8fe-109">Inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-109">Start Eclipse.</span></span>
2. <span data-ttu-id="2c8fe-110">Haga clic en el menú **Help** (Ayuda) y, a continuación, haga clic en **Install New Software** (Instalar nuevo software), como se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![Instalación del Kit de herramientas de Azure para Eclipse][01]
3. <span data-ttu-id="2c8fe-112">En el cuadro de diálogo **Available Software** (Software disponible), en el cuadro de texto **Work with** (Trabajar con), escriba `http://dl.microsoft.com/eclipse` seguido de la tecla **Intro**.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="2c8fe-113">En el panel **Nombre**, active **Kit de herramientas de Azure para Eclipse**, y desactive **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario**.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="2c8fe-114">La pantalla debe parecerse a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="2c8fe-114">Your screen should appear similar to the following:</span></span>
   
    ![Instalación del Kit de herramientas de Azure para Eclipse][02]
5. <span data-ttu-id="2c8fe-116">Si expande el **kit de herramientas de Azure para Eclipse**, verá los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2c8fe-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="2c8fe-117">**Complemento de Application Insights para Java**: este componente permite usar los servicios de análisis y registro de telemetría de Azure para sus aplicaciones e instancias de servidor.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="2c8fe-118">**Filtro de Azure Access Control Service**: este componente proporciona compatibilidad para autenticar a los usuarios de aplicaciones con ACS de Azure, lo que permite poner en práctica escenarios de inicio de sesión único y externalizar la lógica de identidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="2c8fe-119">**Complemento común de Azure**: este componente proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="2c8fe-120">**Explorador de Azure para Eclipse**: este componente proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="2c8fe-121">**Complemento de Azure para Eclipse con Java**: este componente respalda el desarrollo de proyectos que lo ayudan a crear, probar e implementar aplicaciones de Java para la nube de Microsoft Azure en Eclipse y mediante la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="2c8fe-122">**Complemento de Azure Web Apps con Java**: este componente permite implementar aplicaciones web de Java en los contenedores de aplicaciones web de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="2c8fe-123">**Microsoft JDBC Driver 4.2 para SQL Server**: este componente proporciona la API de JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="2c8fe-124">**Paquete para bibliotecas de cliente Apache Qpid de JMS**: este componente ofrece el componente de cliente JMS del proyecto de Apache Qpid para habilitar su aplicación para que use la mensajería de AMQP en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="2c8fe-125">**Paquete para bibliotecas de Microsoft Azure para Java**: este componente proporciona las API para acceder a los servicios de Microsoft Azure, como almacenamiento, service bus, runtime de servicio, etc.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="2c8fe-126">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-126">Click **Next**.</span></span> <span data-ttu-id="2c8fe-127">(Si se producen retrasos inusuales al instalar el kit de herramientas, asegúrese de que la opción **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario** está desactivada.)</span><span class="sxs-lookup"><span data-stu-id="2c8fe-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="2c8fe-128">En el cuadro de diálogo **Install Details** (Detalles de instalación), haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="2c8fe-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![Revisión de los detalles de la instalación][03]
8. <span data-ttu-id="2c8fe-130">En el cuadro de diálogo **Revisar licencias** , revise los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="2c8fe-131">Si acepta los términos de los contratos de licencia, haga clic en **I accept the terms of the license agreements** (Acepto los términos de los contratos de licencia) y luego haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="2c8fe-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="2c8fe-132">(En los pasos restantes se supone que acepta los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="2c8fe-133">Si no acepta los términos de los contratos de licencia, salga del proceso de instalación.)</span><span class="sxs-lookup"><span data-stu-id="2c8fe-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![Revisar licencias][04]
   
    <span data-ttu-id="2c8fe-135">Eclipse descargará e instalará los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![Progreso de la instalación][05]
9. <span data-ttu-id="2c8fe-137">Si se le solicita que reinicie Eclipse para completar la instalación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="2c8fe-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![Reinicio del símbolo del sistema][06]

## <a name="see-also"></a><span data-ttu-id="2c8fe-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2c8fe-139">See Also</span></span>
<span data-ttu-id="2c8fe-140">Para más información acerca de los kits de herramientas de Azure para los IDE de Java, vea los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="2c8fe-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="2c8fe-141">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2c8fe-142">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2c8fe-143">*Instalación del kit de herramientas de Azure para Eclipse (este artículo)*</span><span class="sxs-lookup"><span data-stu-id="2c8fe-143">*Installing the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="2c8fe-144">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2c8fe-145">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="2c8fe-146">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2c8fe-147">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2c8fe-148">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2c8fe-149">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2c8fe-150">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2c8fe-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="2c8fe-151">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure].</span><span class="sxs-lookup"><span data-stu-id="2c8fe-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="2c8fe-152">[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="2c8fe-153">[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="2c8fe-154">[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="2c8fe-155">[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="2c8fe-156">[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="2c8fe-157">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse)</span><span class="sxs-lookup"><span data-stu-id="2c8fe-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="2c8fe-158">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="2c8fe-159">[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="2c8fe-160">[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="2c8fe-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="2c8fe-161">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="2c8fe-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
