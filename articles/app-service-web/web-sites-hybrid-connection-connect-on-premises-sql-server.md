---
title: "Conexión a un servidor SQL local desde una aplicación web en el Servicio de aplicaciones de Azure mediante Conexiones híbridas"
description: "Crear una aplicación web en Microsoft Azure y conectarla a una base de datos de SQL Server local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="a13d7-103">Conexión a un servidor SQL local desde una aplicación web en el Servicio de aplicaciones de Azure mediante Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a13d7-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="a13d7-104">Conexiones híbridas puede conectar Aplicaciones web del [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) con recursos locales que usan puerto TCP estático.</span><span class="sxs-lookup"><span data-stu-id="a13d7-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="a13d7-105">Los recursos admitidos incluyen Microsoft SQL Server, MySQL, API web HTTP, App Service y la mayoría de servicios web personalizados.</span><span class="sxs-lookup"><span data-stu-id="a13d7-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="a13d7-106">En este tutorial aprenderemos a crear un aplicación web del Servicio de aplicaciones en el [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715), a conectar la aplicación web a una base de datos de SQL Server local usando la nueva característica Conexión híbrida, a crear una aplicación ASP.NET simple que usará la conexión híbrida y a implementar la aplicación en la aplicación web del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a13d7-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="a13d7-107">La aplicación web completada en Azure almacena credenciales de usuario en una base de datos de miembros de pertenencia local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="a13d7-108">En el tutorial se asume que no tiene ninguna experiencia anterior con Azure o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a13d7-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="a13d7-109">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de suscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a13d7-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a13d7-110">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a13d7-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="a13d7-111">La parte Aplicaciones web de la característica Conexiones híbridas solo está disponible en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a13d7-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="a13d7-112">Para crear una conexión en Servicios de BizTalk, consulte [Conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="a13d7-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a13d7-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a13d7-113">Prerequisites</span></span>
<span data-ttu-id="a13d7-114">Para completar este tutorial, necesitará los siguientes productos.</span><span class="sxs-lookup"><span data-stu-id="a13d7-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="a13d7-115">Todos están disponibles en versión gratuita, así que puede comenzar a desarrollar en Azure completamente gratis.</span><span class="sxs-lookup"><span data-stu-id="a13d7-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="a13d7-116">**Suscripción de Azure** : para obtener una suscripción gratuita, consulte [Prueba gratuita de Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a13d7-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="a13d7-117">**Visual Studio 2013** : para descargar una versión de evaluación gratuita de Visual Studio 2013, consulte [Descargas de Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="a13d7-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="a13d7-118">Instale esta aplicación antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="a13d7-118">Install this before continuing.</span></span>
* <span data-ttu-id="a13d7-119">**Microsoft .NET Framework 3.5 Service Pack 1**: si su sistema operativo es Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 o Windows Server 2008 R2, puede habilitar este producto en Panel de control > Programas y características > Activar o desactivar las características de Windows.</span><span class="sxs-lookup"><span data-stu-id="a13d7-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="a13d7-120">De lo contrario, puede descargarlo desde el [Centro de descargas de Microsoft](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="a13d7-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="a13d7-121">**SQL Server 2014 Express with Tools** : descargue Microsoft SQL Server Express de forma gratuita en la [página de bases de datos de Plataforma web de Microsoft](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="a13d7-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="a13d7-122">Elija la versión **Express** (no LocalDB).</span><span class="sxs-lookup"><span data-stu-id="a13d7-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="a13d7-123">La versión **Express with Tools** incluye SQL Server Management Studio, que usará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a13d7-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="a13d7-124">**SQL Server Management Studio Express** : este producto se incluye en la descarga de SQL Server 2014 Express with Tools mencionada anteriormente, pero si lo instala por separado, puede descargarlo e instalarlo desde la [página de descargas de SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="a13d7-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="a13d7-125">En este tutorial se supone que tiene una suscripción de Azure, que ha instalado Visual Studio 2013 y que ha instalado o habilitado .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="a13d7-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="a13d7-126">En el tutorial se muestra cómo instalar SQL Server 2014 Express en una configuración que funcione bien con la característica Conexiones híbridas de Azure (una instancia predeterminada con un puerto TCP estático).</span><span class="sxs-lookup"><span data-stu-id="a13d7-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="a13d7-127">Antes de iniciar el tutorial, descargue SQL Server 2014 Express with Tools desde la ubicación mencionada anteriormente sino tiene SQL Server instalado.</span><span class="sxs-lookup"><span data-stu-id="a13d7-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="a13d7-128">Notas</span><span class="sxs-lookup"><span data-stu-id="a13d7-128">Notes</span></span>
<span data-ttu-id="a13d7-129">Para usar una base de datos de SQL Server o SQL Server Express local con una conexión híbrida, es necesario habilitar TCP/IP en un puerto estático.</span><span class="sxs-lookup"><span data-stu-id="a13d7-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="a13d7-130">Las instancias predeterminadas de SQL Server usan el puerto estático 1433, mientras que las instancias con nombre no.</span><span class="sxs-lookup"><span data-stu-id="a13d7-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="a13d7-131">El equipo en el que instala el administrador de conexiones híbridas local:</span><span class="sxs-lookup"><span data-stu-id="a13d7-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="a13d7-132">Debe tener conectividad de salida a Azure a través de:</span><span class="sxs-lookup"><span data-stu-id="a13d7-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="a13d7-133">Port</span><span class="sxs-lookup"><span data-stu-id="a13d7-133">Port</span></span> | <span data-ttu-id="a13d7-134">Porqué</span><span class="sxs-lookup"><span data-stu-id="a13d7-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="a13d7-135">80</span><span class="sxs-lookup"><span data-stu-id="a13d7-135">80</span></span> |<span data-ttu-id="a13d7-136">**Obligatorio** para el puerto HTTP, para la validación de certificados y, de forma opcional, para la conectividad de datos.</span><span class="sxs-lookup"><span data-stu-id="a13d7-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="a13d7-137">443</span><span class="sxs-lookup"><span data-stu-id="a13d7-137">443</span></span> |<span data-ttu-id="a13d7-138">**Opcional** para la conectividad de datos.</span><span class="sxs-lookup"><span data-stu-id="a13d7-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="a13d7-139">Si la conectividad de salida para 443 no está disponible, se usa el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="a13d7-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="a13d7-140">5671 y 9352</span><span class="sxs-lookup"><span data-stu-id="a13d7-140">5671 and 9352</span></span> |<span data-ttu-id="a13d7-141">**Recomendado** , pero opcional para la conectividad de datos.</span><span class="sxs-lookup"><span data-stu-id="a13d7-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="a13d7-142">Tenga en cuenta que este modo obtiene mayor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a13d7-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="a13d7-143">Si la conectividad de salida para estos puertos no está disponible, se usa el puerto TCP 443.</span><span class="sxs-lookup"><span data-stu-id="a13d7-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="a13d7-144">Debe poder establecer comunicación con el *hostname*:*número de puerto* de su recurso local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="a13d7-145">En estos pasos de este artículo se supone que usa el explorador del equipo que hospeda el agente de conexiones híbridas local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="a13d7-146">Si ya tiene SQL Server instalado en una configuración y en un entorno que cumple las condiciones descritas anteriormente, puede continuar y empezar con [Creación de una base de datos de SQL Server local](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="a13d7-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="a13d7-147">A.</span><span class="sxs-lookup"><span data-stu-id="a13d7-147">A.</span></span> <span data-ttu-id="a13d7-148">Instalación de SQL Server Express, habilitación de TCP/IP y creación de una base de datos SQL Server local</span><span class="sxs-lookup"><span data-stu-id="a13d7-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="a13d7-149">En esta sección se muestra cómo instalar SQL Server Express, habilitar TCP/IP y crear una base de datos de forma que la aplicación web funcione con el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a13d7-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="a13d7-150">Instalación de SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="a13d7-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="a13d7-151">Para instalar SQL Server Express, ejecute el archivo **SQLEXPRWT_x64_ENU.exe** o **SQLEXPR_x86_ENU.exe** que descargó.</span><span class="sxs-lookup"><span data-stu-id="a13d7-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="a13d7-152">Aparecerá el asistente Centro de instalación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a13d7-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="a13d7-154">Elija **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="a13d7-155">Siga las instrucciones, aceptando las elecciones y configuraciones predeterminadas, hasta llegar a la página **Configuración de instancia** .</span><span class="sxs-lookup"><span data-stu-id="a13d7-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="a13d7-156">En la página **Configuración de instancia**, elija **Instancia predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="a13d7-158">De forma predeterminada, la instancia predeterminada de SQL Server escucha solicitudes de clientes de SQL Server en el puerto estático 1433, que es el que requiere la característica Conexiones híbridas.</span><span class="sxs-lookup"><span data-stu-id="a13d7-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="a13d7-159">Las instancias con nombre usan puertos dinámicos y UDP, que Conexiones híbridas no admite.</span><span class="sxs-lookup"><span data-stu-id="a13d7-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="a13d7-160">Acepte las configuraciones predeterminadas en la página **Configuración del servidor** .</span><span class="sxs-lookup"><span data-stu-id="a13d7-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="a13d7-161">En la página **Configuración del Motor de base de datos**, bajo **Modo de autenticación**, elija **Modo mixto (autenticación de SQL Server y de Windows)** y proporcione una contraseña.</span><span class="sxs-lookup"><span data-stu-id="a13d7-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="a13d7-163">En este tutorial se usará la autenticación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a13d7-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="a13d7-164">Asegúrese de recordar la contraseña proporcionada, ya que la necesitará más tarde.</span><span class="sxs-lookup"><span data-stu-id="a13d7-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="a13d7-165">Recorra el resto del asistente para completar la instalación.</span><span class="sxs-lookup"><span data-stu-id="a13d7-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="a13d7-166">Habilitar TCP/IP</span><span class="sxs-lookup"><span data-stu-id="a13d7-166">Enable TCP/IP</span></span>
<span data-ttu-id="a13d7-167">Para habilitar TCP/IP, usará el Administrador de configuración de SQL Server, que se instaló al instalar SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="a13d7-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="a13d7-168">Siga los pasos que figuran en [Habilitar el protocolo de red TCP/IP para SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="a13d7-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="a13d7-169">Creación de una base de datos de SQL Server local</span><span class="sxs-lookup"><span data-stu-id="a13d7-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="a13d7-170">La aplicación web de Visual Studio requiere una base de datos de pertenencia a la que pueda acceder Azure.</span><span class="sxs-lookup"><span data-stu-id="a13d7-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="a13d7-171">Para ello, se necesita una base de datos de SQL Server o SQL Server Express (no la base de datos LocalDB que usa la plantilla MVC de forma predeterminada), por lo que seguidamente creará la base de datos de pertenencia.</span><span class="sxs-lookup"><span data-stu-id="a13d7-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="a13d7-172">En SQL Server Management Studio, conéctese al servidor SQL Server que acaba de instalar.</span><span class="sxs-lookup"><span data-stu-id="a13d7-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="a13d7-173">(Si el cuadro de diálogo **Conectar al servidor** no se abre automáticamente, vaya al **Explorador de objetos** en el panel izquierdo, haga clic en **Conectar** y en **Motor de la base de datos**). ![Conectar al servidor][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="a13d7-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="a13d7-174">En **Tipo de servidor**, elija **Motor de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="a13d7-175">En **Nombre de servidor**, puede usar **localhost** o el nombre del equipo que esté usando.</span><span class="sxs-lookup"><span data-stu-id="a13d7-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="a13d7-176">Elija **Autenticación de SQL Server**y después inicie sesión con el nombre de usuario sa y la contraseña que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a13d7-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="a13d7-177">Para crear una base de datos usando SQL Server Management Studio, haga clic con el botón derecho en **Base de datos** en el Explorador de objetos y, a continuación, haga clic en **Nueva base de datos**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="a13d7-179">En el cuadro de diálogo **Nueva base de datos**, escriba MembershipDB como nombre de la base de datos y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="a13d7-181">Tenga en cuenta que, llegados a este punto, no realiza ningún cambio en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a13d7-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="a13d7-182">La aplicación web agregará más tarde la información de pertenencia automáticamente cuando se ejecute.</span><span class="sxs-lookup"><span data-stu-id="a13d7-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="a13d7-183">En el Explorador de objetos, si expande **Bases de datos**, verá que se ha creado la base de datos de pertenencia.</span><span class="sxs-lookup"><span data-stu-id="a13d7-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="a13d7-185">B.</span><span class="sxs-lookup"><span data-stu-id="a13d7-185">B.</span></span> <span data-ttu-id="a13d7-186">Creación de una aplicación web en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a13d7-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="a13d7-187">Si ya ha creado una aplicación web en el Portal de Azure que desea usar en este tutorial, puede omitir este paso e ir directamente a [Creación de una conexión híbrida y un servicio de BizTalk](#CreateHC) y continuar desde ahí.</span><span class="sxs-lookup"><span data-stu-id="a13d7-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="a13d7-188">En [Azure Portal](https://portal.azure.com), haga clic en **Nuevo** > **Web y móvil** > **Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="a13d7-190">Configure su aplicación web y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="a13d7-192">Transcurridos unos segundos, la aplicación web se creará y aparecerá su hoja de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a13d7-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="a13d7-193">La hoja es un panel que se desplaza en vertical y que le permite administrar su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a13d7-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="a13d7-195">Para comprobar que la aplicación web está activa, puede hacer clic en el icono **Examinar** para mostrar la página predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a13d7-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="a13d7-196">A continuación, creará una conexión híbrida y un servicio de BizTalk para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a13d7-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="a13d7-197">C.</span><span class="sxs-lookup"><span data-stu-id="a13d7-197">C.</span></span> <span data-ttu-id="a13d7-198">Creación de una conexión híbrida y un servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="a13d7-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="a13d7-199">En el portal, vaya a configuración y haga clic en **Redes** > **Configurar los puntos de conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexiones híbridas][CreateHCHCIcon]
2. <span data-ttu-id="a13d7-201">En la hoja de conexiones híbridas, haga clic en **Agregar** > **Nueva conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="a13d7-202">En la hoja **Crear conexión híbrida** :</span><span class="sxs-lookup"><span data-stu-id="a13d7-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="a13d7-203">En **Nombre**, proporcione un nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="a13d7-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="a13d7-204">En **Nombre de host**, escriba el nombre del equipo del equipo host de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a13d7-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="a13d7-205">En **Puerto**, escriba 1433 (el puerto predeterminado para SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a13d7-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="a13d7-206">Haga clic en **Servicio de BizTalk** > **Nuevo servicio de BizTalk** y escriba un nombre para el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a13d7-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="a13d7-208">Haga clic en **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="a13d7-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="a13d7-209">Al finalizar el proceso, el área **Notificaciones** emitirá el mensaje **CORRECTO** parpadeante en color verde y la hoja **Conexión híbrida** mostrará la conexión híbrida nueva con el estado **No conectado**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="a13d7-211">Llegados a este punto, ha completado una parte importante de la infraestructura de conexión híbrida en la nube.</span><span class="sxs-lookup"><span data-stu-id="a13d7-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="a13d7-212">A continuación, creará la parte local correspondiente.</span><span class="sxs-lookup"><span data-stu-id="a13d7-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="a13d7-213">D.</span><span class="sxs-lookup"><span data-stu-id="a13d7-213">D.</span></span> <span data-ttu-id="a13d7-214">Instalación del Administrador de conexiones híbridas local para realizar la conexión</span><span class="sxs-lookup"><span data-stu-id="a13d7-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="a13d7-215">Ahora que la infraestructura de la conexión híbrida se ha completado, creará una aplicación web que la use.</span><span class="sxs-lookup"><span data-stu-id="a13d7-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="a13d7-216">E.</span><span class="sxs-lookup"><span data-stu-id="a13d7-216">E.</span></span> <span data-ttu-id="a13d7-217">Creación de un proyecto web ASP.NET básico, edición de la cadena de conexión de base de datos y ejecución del proyecto localmente</span><span class="sxs-lookup"><span data-stu-id="a13d7-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="a13d7-218">Creación de un proyecto ASP.NET básico</span><span class="sxs-lookup"><span data-stu-id="a13d7-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="a13d7-219">En Visual Studio, en el menú **Archivo** , cree un proyecto nuevo:</span><span class="sxs-lookup"><span data-stu-id="a13d7-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="a13d7-221">En la sección **Plantillas** del cuadro de diálogo **Nuevo proyecto**, seleccione **Web**, elija **Aplicación web de ASP.NET** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="a13d7-223">En el cuadro de diálogo **Nuevo proyecto de ASP.NET**, elija **MVC** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="a13d7-225">Cuando el proyecto se haya creado, aparecerá la página Léame de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a13d7-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="a13d7-226">No ejecute el proyecto web todavía.</span><span class="sxs-lookup"><span data-stu-id="a13d7-226">Do not run the web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="a13d7-228">Edición de la cadena de conexión de la base de datos para la aplicación</span><span class="sxs-lookup"><span data-stu-id="a13d7-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="a13d7-229">En este paso editará la cadena de conexión que indica a la aplicación dónde buscar la base de datos de SQL Server Express local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="a13d7-230">La cadena de conexión es un archivo Web.config de la aplicación que contiene información de configuración para dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="a13d7-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="a13d7-231">Para garantizar que la aplicación usa la base de datos creada en SQL Server Express y no la base de datos LocalDB predeterminada de Visual Studio, es importante que complete este paso antes de ejecutar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a13d7-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="a13d7-232">En el Explorador de soluciones, haga doble clic en el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="a13d7-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="a13d7-234">Edite la sección **connectionStrings** para apuntar a la base de datos de SQL Server en la máquina local, siguiendo la sintaxis del ejemplo que se muestra continuación:</span><span class="sxs-lookup"><span data-stu-id="a13d7-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Cadena de conexión][HCVSConnectionString]
   
    <span data-ttu-id="a13d7-236">Cuando escriba la cadena de conexión, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a13d7-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="a13d7-237">Si se está conectando a una instancia con nombre en lugar de a una instancia predeterminada (por ejemplo SuServidor\SQLEXPRESS), debe configurar su servidor SQL Server para usar puertos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a13d7-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="a13d7-238">Para obtener información sobre la configuración de puertos estáticos, consulte [Cómo configurar SQL Server para que escuche en un puerto específico](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="a13d7-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="a13d7-239">De forma predeterminada, las instancias con nombre usan puertos dinámicos y UDP, que Conexiones híbridas no admite.</span><span class="sxs-lookup"><span data-stu-id="a13d7-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="a13d7-240">Es recomendable que especifique el puerto (1433 de forma predeterminada, como se muestra en el ejemplo) en la cadena de conexión de forma que pueda asegurarse de que su servidor SQL Server local tiene la funcionalidad TCP habilitada y usa el puerto correcto.</span><span class="sxs-lookup"><span data-stu-id="a13d7-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="a13d7-241">Recuerde usar Autenticación de SQL Server para conectarse, especificando el identificador y la contraseña del usuario en la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="a13d7-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="a13d7-242">Haga clic en **Guardar** en Visual Studio para guardar el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="a13d7-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="a13d7-243">Ejecución del proyecto localmente y registro de un nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="a13d7-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="a13d7-244">Ahora, ejecute el nuevo proyecto web localmente haciendo clic en el botón Examinar que se encuentra debajo de Depurar.</span><span class="sxs-lookup"><span data-stu-id="a13d7-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="a13d7-245">En este ejemplo se usa Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a13d7-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="a13d7-247">En la esquina superior derecha de la página web predeterminada, elija **Registrar** para registrar una cuenta nueva:</span><span class="sxs-lookup"><span data-stu-id="a13d7-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="a13d7-249">Escriba un nombre de usuario y una contraseña:</span><span class="sxs-lookup"><span data-stu-id="a13d7-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="a13d7-251">Esta operación creará automáticamente una base de datos en su servidor SQL Server local que hospedará la información de pertenencia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a13d7-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="a13d7-252">Una de las tablas (**dbo.AspNetUsers**) contiene las credenciales de usuario de la aplicación web como las que acaba de introducir.</span><span class="sxs-lookup"><span data-stu-id="a13d7-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="a13d7-253">Verá esta tabla posteriormente en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="a13d7-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="a13d7-254">Cierre la ventana del explorador de la página web predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a13d7-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="a13d7-255">Esta operación detendrá la aplicación en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a13d7-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="a13d7-256">Ahora está preparado para continuar con el paso siguiente, que consiste en publicar la aplicación en Azure y probarla.</span><span class="sxs-lookup"><span data-stu-id="a13d7-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="a13d7-257">F.</span><span class="sxs-lookup"><span data-stu-id="a13d7-257">F.</span></span> <span data-ttu-id="a13d7-258">Publicación de la aplicación web en Azure y prueba de la misma</span><span class="sxs-lookup"><span data-stu-id="a13d7-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="a13d7-259">Ahora publicará la aplicación en su aplicación web del Servicio de aplicaciones y después la probará para ver cómo se usa la conexión híbrida que configuró anteriormente para conectar la aplicación web a la base de datos en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="a13d7-260">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a13d7-260">Publish the web application</span></span>
1. <span data-ttu-id="a13d7-261">Puede descargar el perfil de publicación para la aplicación web del Servicio de aplicaciones en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a13d7-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="a13d7-262">En la hoja correspondiente a su aplicación web, haga clic en **Obtener perfil de publicación**y guarde el archivo en su equipo.</span><span class="sxs-lookup"><span data-stu-id="a13d7-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Descargar archivo de publicación][PortalDownloadPublishProfile]
   
    <span data-ttu-id="a13d7-264">A continuación, importará este archivo en la aplicación web de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a13d7-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="a13d7-265">En Visual Studio, haga clic con el botón secundario en el nombre del proyecto en el Explorador de soluciones y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="a13d7-267">En el cuadro de diálogo **Publicación web**, en la pestaña **Perfil**, elija **Importar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Importar][HCVSPublishWebDialogImport]
4. <span data-ttu-id="a13d7-269">Examine el perfil de publicación descargado, selecciónelo y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Browse to profile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="a13d7-271">Su información de publicación se importará y mostrará en la pestaña **Conexión** del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a13d7-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Haga clic en Publicar.][HCVSClickPublish]
   
    <span data-ttu-id="a13d7-273">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="a13d7-274">Cuando la publicación se complete, el explorador se iniciará y mostrará su, ahora, aplicación de ASP.NET, ¡con la diferencia de que ahora está activa en la nube de Azure!</span><span class="sxs-lookup"><span data-stu-id="a13d7-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="a13d7-275">A continuación, usará la aplicación web activa para ver su conexión híbrida en acción.</span><span class="sxs-lookup"><span data-stu-id="a13d7-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="a13d7-276">Prueba de la aplicación web completada en Azure</span><span class="sxs-lookup"><span data-stu-id="a13d7-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="a13d7-277">En la parte superior de la página web en Azure, elija **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="a13d7-279">La aplicación web del Servicio de aplicaciones ahora estará conectada a la base de datos de pertenencia de la aplicación web en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="a13d7-280">Para comprobarlo, inicie sesión con las mismas credenciales que introdujo en la base de datos local anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a13d7-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="a13d7-282">Para seguir probando su nueva conexión híbrida, cierre la sesión de la aplicación web de Azure y regístrese como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="a13d7-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="a13d7-283">Proporcione un nuevo nombre de usuario y contraseña y, a continuación, haga clic en **Registrarse**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="a13d7-285">Para comprobar que las credenciales del nuevo usuario se han almacenado en la base de datos local a través de la conexión híbrida, abra SQL Management Studio en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="a13d7-286">En el Explorador de objetos, expanda la base de datos **MembershipDB** y, a continuación, **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="a13d7-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="a13d7-287">Haga clic con el botón derecho en la tabla de pertenencia **dbo.AspNetUsers** y elija **Seleccionar las primeras 1000 filas** para ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="a13d7-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![View the results][HCTestSSMSTree]
5. <span data-ttu-id="a13d7-289">La tabla de pertenencia local ahora muestra ambas cuentas, la que creó localmente y la que creó en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="a13d7-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="a13d7-290">La que creó en la nube se ha guardado en la base de datos local a través de la característica Conexión híbrida de Azure.</span><span class="sxs-lookup"><span data-stu-id="a13d7-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="a13d7-292">Ya ha creado e implementado una aplicación web ASP.NET que usa una conexión híbrida entre una aplicación web y la nube de Azure y una base de datos de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="a13d7-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="a13d7-293">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="a13d7-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="a13d7-294">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a13d7-294">See Also</span></span>
[<span data-ttu-id="a13d7-295">Introducción a las conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a13d7-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="a13d7-296">Josh Twist presenta las conexiones híbridas (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="a13d7-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="a13d7-297">Introducción a las conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a13d7-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="a13d7-298">Servicios de BizTalk: pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a13d7-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="a13d7-299">Creación de una nube híbrida del mundo real con una perfecta portabilidad de aplicaciones (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="a13d7-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="a13d7-300">Acceso a recursos locales mediante conexiones híbridas en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a13d7-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="a13d7-301">Introducción a la identidad de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a13d7-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
