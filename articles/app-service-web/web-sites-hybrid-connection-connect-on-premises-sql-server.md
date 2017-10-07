---
title: "aaaConnect tooon local SQL Server desde una aplicación web en el servicio de aplicaciones de Azure usando conexiones híbridas"
description: "Crear una aplicación web en Microsoft Azure y conectar base de datos de SQL Server de tooan local"
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="391b2-103">Conectar SQL Server local tooon desde una aplicación web en el servicio de aplicación de Azure usando conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="391b2-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="391b2-104">Pueden conectar las conexiones híbridas [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) recursos de tooon locales de aplicaciones Web que utilizan un puerto TCP estático.</span><span class="sxs-lookup"><span data-stu-id="391b2-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="391b2-105">Los recursos admitidos incluyen Microsoft SQL Server, MySQL, API web HTTP, App Service y la mayoría de servicios web personalizados.</span><span class="sxs-lookup"><span data-stu-id="391b2-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="391b2-106">En este tutorial, obtendrá información sobre cómo toocreate un servicio de aplicación web aplicación Hola [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715), conectar hello web app tooyour en instalaciones locales SQL Server base de datos mediante la nueva característica de conexión híbrida hello, cree un ASP.NET simple aplicación que usará la conexión híbrida de hello y, implementar Hola aplicación toohello aplicación de servicio de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="391b2-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="391b2-107">Hola completado web app en Azure almacena las credenciales de usuario en una base de datos de pertenencia en una ubicación local.</span><span class="sxs-lookup"><span data-stu-id="391b2-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="391b2-108">tutorial de Hello no supone ninguna experiencia previa con Azure o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="391b2-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="391b2-109">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="391b2-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="391b2-110">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="391b2-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="391b2-111">parte de las aplicaciones Web de Hola de característica de conexiones híbridas de hello solo está disponible en hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="391b2-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="391b2-112">toocreate una conexión de servicios de BizTalk, consulte [conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="391b2-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="391b2-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="391b2-113">Prerequisites</span></span>
<span data-ttu-id="391b2-114">toocomplete este tutorial, necesitará Hola después de productos.</span><span class="sxs-lookup"><span data-stu-id="391b2-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="391b2-115">Todos están disponibles en versión gratuita, así que puede comenzar a desarrollar en Azure completamente gratis.</span><span class="sxs-lookup"><span data-stu-id="391b2-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="391b2-116">**Suscripción de Azure** : para obtener una suscripción gratuita, consulte [Prueba gratuita de Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="391b2-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="391b2-117">**Visual Studio 2013** -toodownload una versión de prueba gratuita de Visual Studio 2013, vea [descargas de Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="391b2-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="391b2-118">Instale esta aplicación antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="391b2-118">Install this before continuing.</span></span>
* <span data-ttu-id="391b2-119">**Microsoft .NET Framework 3.5 Service Pack 1**: si su sistema operativo es Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 o Windows Server 2008 R2, puede habilitar este producto en Panel de control &gt; Programas y características &gt; Activar o desactivar las características de Windows.</span><span class="sxs-lookup"><span data-stu-id="391b2-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="391b2-120">En caso contrario, puede descargarlo en hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="391b2-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="391b2-121">**SQL Server 2014 Express con herramientas** -descargar Microsoft SQL Server Express de forma gratuita en hello [página de base de datos de Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="391b2-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="391b2-122">Elija hello **Express** (no LocalDB) versión.</span><span class="sxs-lookup"><span data-stu-id="391b2-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="391b2-123">Hola **Express with Tools** versión incluye SQL Server Management Studio, que se usará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="391b2-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="391b2-124">**SQL Server Management Studio Express** : Esto se incluye con SQL Server 2014 Express de hello en la descarga de herramientas se ha mencionado anteriormente, pero si necesita tooinstall se por separado, se puede descargar e instalarlo desde hello [SQL Server Express página de descarga de](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="391b2-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="391b2-125">tutorial de Hola se da por supuesto que tiene una suscripción a Azure que ha instalado Visual Studio 2013, y que ha instalado o habilitado .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="391b2-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="391b2-126">Hola tutorial le mostrará cómo tooinstall SQL Server 2014 Express en una configuración que funciona bien con las conexiones híbridas de Azure Hola característica (una instancia predeterminada con un puerto TCP estático).</span><span class="sxs-lookup"><span data-stu-id="391b2-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="391b2-127">Antes de iniciar el tutorial de hello, descargar SQL Server 2014 Express con herramientas de ubicación de hello que ya se mencionó anteriormente, si no tiene instalado SQL Server.</span><span class="sxs-lookup"><span data-stu-id="391b2-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="391b2-128">Notas</span><span class="sxs-lookup"><span data-stu-id="391b2-128">Notes</span></span>
<span data-ttu-id="391b2-129">toouse un local SQL Server o base de datos de SQL Server Express con una conexión híbrida, TCP/IP debe toobe habilitado en un puerto estático.</span><span class="sxs-lookup"><span data-stu-id="391b2-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="391b2-130">Las instancias predeterminadas de SQL Server usan el puerto estático 1433, mientras que las instancias con nombre no.</span><span class="sxs-lookup"><span data-stu-id="391b2-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="391b2-131">equipo de Hello en el que instale el agente de administrador de conexiones híbridas local hello:</span><span class="sxs-lookup"><span data-stu-id="391b2-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="391b2-132">Debe tener conectividad saliente tooAzure sobre:</span><span class="sxs-lookup"><span data-stu-id="391b2-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="391b2-133">Port</span><span class="sxs-lookup"><span data-stu-id="391b2-133">Port</span></span> | <span data-ttu-id="391b2-134">Porqué</span><span class="sxs-lookup"><span data-stu-id="391b2-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="391b2-135">80</span><span class="sxs-lookup"><span data-stu-id="391b2-135">80</span></span> |<span data-ttu-id="391b2-136">**Obligatorio** para el puerto HTTP, para la validación de certificados y, de forma opcional, para la conectividad de datos.</span><span class="sxs-lookup"><span data-stu-id="391b2-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="391b2-137">443</span><span class="sxs-lookup"><span data-stu-id="391b2-137">443</span></span> |<span data-ttu-id="391b2-138">**Opcional** para la conectividad de datos.</span><span class="sxs-lookup"><span data-stu-id="391b2-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="391b2-139">Si too443 conectividad saliente no está disponible, se utiliza el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="391b2-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="391b2-140">5671 y 9352</span><span class="sxs-lookup"><span data-stu-id="391b2-140">5671 and 9352</span></span> |<span data-ttu-id="391b2-141">**Recomendado** , pero opcional para la conectividad de datos.</span><span class="sxs-lookup"><span data-stu-id="391b2-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="391b2-142">Tenga en cuenta que este modo obtiene mayor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="391b2-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="391b2-143">Si los puertos toothese conectividad saliente no está disponible, se utiliza el puerto TCP 443.</span><span class="sxs-lookup"><span data-stu-id="391b2-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="391b2-144">Debe ser capaz de tooreach hello *hostname*:*portnumber* de su recurso local.</span><span class="sxs-lookup"><span data-stu-id="391b2-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="391b2-145">pasos de Hello en este artículo se supone que está usando explorador Hola desde equipo Hola que hospedará el agente de conexión híbrida de hello local.</span><span class="sxs-lookup"><span data-stu-id="391b2-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="391b2-146">Si ya tiene SQL Server instalado en una configuración y en un entorno que cumple las condiciones de Hola se ha descrito anteriormente, puede saltarse lecciones y empezar con [crear una base de datos de SQL Server local](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="391b2-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="391b2-147">A.</span><span class="sxs-lookup"><span data-stu-id="391b2-147">A.</span></span> <span data-ttu-id="391b2-148">Instalación de SQL Server Express, habilitación de TCP/IP y creación de una base de datos SQL Server local</span><span class="sxs-lookup"><span data-stu-id="391b2-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="391b2-149">Esta sección muestra cómo habilitar TCP/IP tooinstall SQL Server Express y crear una base de datos para que funcione la aplicación web con hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="391b2-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="391b2-150">Instalación de SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="391b2-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="391b2-151">tooinstall SQL Server Express, ejecute hello **SQLEXPRWT_x64_ENU.exe** o **SQLEXPR_x86_ENU.exe** archivo que descargó.</span><span class="sxs-lookup"><span data-stu-id="391b2-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="391b2-152">aparece el Asistente de Hello centro de instalación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="391b2-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="391b2-154">Elija **nueva instalación SQL Server independiente o agregar la instalación existente de características tooan**.</span><span class="sxs-lookup"><span data-stu-id="391b2-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="391b2-155">Siga las instrucciones de hello, acepte las opciones predeterminadas hello y la configuración, hasta llegar toohello **configuración de instancia** página.</span><span class="sxs-lookup"><span data-stu-id="391b2-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="391b2-156">En hello **configuración de instancia** página, elija **instancia predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="391b2-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="391b2-158">De forma predeterminada, instancia predeterminada de Hola de SQL Server escucha las solicitudes de clientes de SQL Server en el puerto 1433, que es qué hello conexiones híbridas requiere la característica.</span><span class="sxs-lookup"><span data-stu-id="391b2-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="391b2-159">Las instancias con nombre usan puertos dinámicos y UDP, que Conexiones híbridas no admite.</span><span class="sxs-lookup"><span data-stu-id="391b2-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="391b2-160">Acepte los valores predeterminados de hello en hello **configuración del servidor** página.</span><span class="sxs-lookup"><span data-stu-id="391b2-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="391b2-161">En hello **configuración del motor de base de datos** página, en **modo de autenticación**, elija **modo mixto (autenticación de SQL Server y la autenticación de Windows)**y proporcionar una contraseña.</span><span class="sxs-lookup"><span data-stu-id="391b2-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="391b2-163">En este tutorial se usará la autenticación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="391b2-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="391b2-164">Estar seguro tooremember Hola por contraseña que proporcione, ya que la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="391b2-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="391b2-165">Paso a paso a través de rest de Hola de instalación de hello Asistente toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="391b2-166">Habilitar TCP/IP</span><span class="sxs-lookup"><span data-stu-id="391b2-166">Enable TCP/IP</span></span>
<span data-ttu-id="391b2-167">tooenable TCP/IP, se usará el Administrador de configuración de SQL Server, que se instala al instalar SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="391b2-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="391b2-168">Siga los pasos de hello en [habilitar el protocolo de red TCP/IP para SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="391b2-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="391b2-169">Creación de una base de datos de SQL Server local</span><span class="sxs-lookup"><span data-stu-id="391b2-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="391b2-170">La aplicación web de Visual Studio requiere una base de datos de pertenencia a la que pueda acceder Azure.</span><span class="sxs-lookup"><span data-stu-id="391b2-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="391b2-171">Esto requiere una base de datos de SQL Server o SQL Server Express (no Hola LocalDB base de datos que Hola usos de plantilla MVC predeterminada), por lo que podrá crear base de datos de pertenencia de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="391b2-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="391b2-172">En SQL Server Management Studio, conéctese toohello recién instalada de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="391b2-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="391b2-173">(Si hello **conectar tooServer** cuadro de diálogo no aparece automáticamente, navegue demasiado**Explorador de objetos** en el panel izquierdo de hello, haga clic en **conectar**y, a continuación, haga clic en **Motor de base de datos**.) ![Conectar tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="391b2-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="391b2-174">En **Tipo de servidor**, elija **Motor de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="391b2-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="391b2-175">Para **nombre del servidor**, puede usar **localhost** Hola de u Hola equipo que está usando.</span><span class="sxs-lookup"><span data-stu-id="391b2-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="391b2-176">Elija **autenticación de SQL Server**y, a continuación, inicie sesión con el nombre de usuario de sa de Hola y Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="391b2-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="391b2-177">toocreate una nueva base de datos mediante el uso de SQL Server Management Studio, haga clic en **bases de datos** en el Explorador de objetos y, a continuación, haga clic en **nueva base de datos**.</span><span class="sxs-lookup"><span data-stu-id="391b2-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="391b2-179">Hola **nueva base de datos** cuadro de diálogo, escriba MembershipDB de nombre de base de datos de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="391b2-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="391b2-181">Tenga en cuenta que no realiza ninguna base de datos de toohello de cambios en este momento.</span><span class="sxs-lookup"><span data-stu-id="391b2-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="391b2-182">información de pertenencia de Hola se agregará automáticamente más tarde mediante la aplicación web cuando se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="391b2-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="391b2-183">En el Explorador de objetos, si expande **bases de datos**, verá esa base de datos de pertenencia de Hola se ha creado.</span><span class="sxs-lookup"><span data-stu-id="391b2-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="391b2-185">B.</span><span class="sxs-lookup"><span data-stu-id="391b2-185">B.</span></span> <span data-ttu-id="391b2-186">Crear una aplicación web en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="391b2-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="391b2-187">Si ya ha creado una aplicación web en hello Portal de Azure que quiere toouse de este tutorial, puede pasar demasiado[crear una conexión híbrida y un BizTalk Service](#CreateHC) y continuar desde allí.</span><span class="sxs-lookup"><span data-stu-id="391b2-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="391b2-188">Hola [Portal de Azure](https://portal.azure.com), haga clic en **New** > **Web y móvil** > **aplicación Web**.</span><span class="sxs-lookup"><span data-stu-id="391b2-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="391b2-190">Configure su aplicación web y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="391b2-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="391b2-192">Después de unos segundos, se crea la aplicación web de hello y aparece su hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="391b2-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="391b2-193">hoja de Hello es un panel puede desplazar verticalmente que le permite administrar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="391b2-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="391b2-195">aplicación web de tooverify hello es en vivo, puede hacer clic en hello **examinar** página predeterminada de icono toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="391b2-196">A continuación, creará una conexión híbrida y un servicio de BizTalk para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="391b2-197">C.</span><span class="sxs-lookup"><span data-stu-id="391b2-197">C.</span></span> <span data-ttu-id="391b2-198">Creación de una conexión híbrida y un servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="391b2-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="391b2-199">Hola Portal, vaya toosettings atrás y haga clic en **red** > **configurar los extremos de conexión híbrida**.</span><span class="sxs-lookup"><span data-stu-id="391b2-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexiones híbridas][CreateHCHCIcon]
2. <span data-ttu-id="391b2-201">En la hoja de conexiones híbridas de hello, haga clic en **agregar** > **conexión híbrida nueva**.</span><span class="sxs-lookup"><span data-stu-id="391b2-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="391b2-202">En hello **crear conexión híbrida** hoja:</span><span class="sxs-lookup"><span data-stu-id="391b2-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="391b2-203">Para **nombre**, proporcione un nombre para la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="391b2-204">Para **Hostname**, escriba Hola nombre de equipo del equipo de host de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="391b2-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="391b2-205">Para **puerto**, escriba 1433 (puerto de hello predeterminado para SQL Server).</span><span class="sxs-lookup"><span data-stu-id="391b2-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="391b2-206">Haga clic en **BizTalk Service** > **nuevo servicio de BizTalk** y escriba un nombre para el servicio de BizTalk de hello.</span><span class="sxs-lookup"><span data-stu-id="391b2-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="391b2-208">Haga clic en **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="391b2-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="391b2-209">Cuando el proceso de hello finalice, hello **notificaciones** área parpadeará en un color verde **correcto** hello y **conexión híbrida** hoja mostrará conexión híbrida nueva de hello con Hola estado como **no conectado**.</span><span class="sxs-lookup"><span data-stu-id="391b2-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="391b2-211">En este momento, ha completado una parte importante de la infraestructura de conexión de hello en la nube híbrida.</span><span class="sxs-lookup"><span data-stu-id="391b2-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="391b2-212">A continuación, creará la parte local correspondiente.</span><span class="sxs-lookup"><span data-stu-id="391b2-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="391b2-213">D.</span><span class="sxs-lookup"><span data-stu-id="391b2-213">D.</span></span> <span data-ttu-id="391b2-214">Instalar Hola local Administrador de conexiones híbridas toocomplete Hola conexión</span><span class="sxs-lookup"><span data-stu-id="391b2-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="391b2-215">Ahora está completa esa infraestructura de conexión híbrida de hello, creará una aplicación web que lo utiliza.</span><span class="sxs-lookup"><span data-stu-id="391b2-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="391b2-216">E.</span><span class="sxs-lookup"><span data-stu-id="391b2-216">E.</span></span> <span data-ttu-id="391b2-217">Cree un proyecto web ASP.NET básico, editar cadena de conexión de base de datos de Hola y ejecutar proyectos de hello localmente</span><span class="sxs-lookup"><span data-stu-id="391b2-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="391b2-218">Creación de un proyecto ASP.NET básico</span><span class="sxs-lookup"><span data-stu-id="391b2-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="391b2-219">En Visual Studio, en hello **archivo** menú, cree un nuevo proyecto:</span><span class="sxs-lookup"><span data-stu-id="391b2-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="391b2-221">Hola **plantillas** sección de hello **nuevo proyecto** cuadro de diálogo, seleccione **Web** y elija **aplicación Web ASP.NET**y, a continuación, haga clic en  **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="391b2-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="391b2-223">Hola **nuevo proyecto ASP.NET** cuadro de diálogo, elija **MVC**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="391b2-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="391b2-225">Cuando se ha creado el proyecto de hello, aparece la página del archivo Léame de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="391b2-226">No ejecute proyecto web de hello todavía.</span><span class="sxs-lookup"><span data-stu-id="391b2-226">Do not run hello web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="391b2-228">Editar cadena de conexión de base de datos de hello para la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="391b2-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="391b2-229">En este paso, editar cadena de conexión de Hola que le indica a la aplicación donde toofind local SQL Server Express base de datos.</span><span class="sxs-lookup"><span data-stu-id="391b2-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="391b2-230">cadena de conexión de Hello es en el archivo Web.config de la aplicación hello, que contiene información de configuración de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="391b2-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="391b2-231">tooensure que la aplicación utiliza la base de datos de Hola que creó en SQL Server Express, no hello y uno en LocalDB predeterminada de Visual Studio, es importante que complete este paso antes de ejecutar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="391b2-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="391b2-232">En el Explorador de soluciones, haga doble clic en el archivo Web.config de Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="391b2-234">Editar hello **connectionStrings** base de datos de sección toopoint toohello SQL Server en el equipo local, la sintaxis de hello en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="391b2-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Cadena de conexión][HCVSConnectionString]
   
    <span data-ttu-id="391b2-236">Cuando se crea la cadena de conexión de hello, tenga en siguiente Hola de cuenta:</span><span class="sxs-lookup"><span data-stu-id="391b2-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="391b2-237">Si va a conectar tooa con el nombre de instancia en lugar de una instancia predeterminada (por ejemplo, YourServer\SQLEXPRESS), debe configurar los puertos estáticos toouse de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="391b2-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="391b2-238">Para obtener información acerca de cómo configurar puertos estáticos, vea [cómo tooconfigure toolisten de SQL Server en un puerto específico](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="391b2-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="391b2-239">De forma predeterminada, las instancias con nombre usan puertos dinámicos y UDP, que Conexiones híbridas no admite.</span><span class="sxs-lookup"><span data-stu-id="391b2-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="391b2-240">Se recomienda que especifique Hola puerto (1433 de forma predeterminada, tal como se muestra en el ejemplo de Hola) en la cadena de conexión de Hola por lo que puede estar seguro de que el servidor SQL Server local tiene TCP habilitado y está utilizando el puerto correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="391b2-241">Recuerde tooconnect de autenticación de SQL Server toouse, especificando el Id. de usuario de Hola y la contraseña en la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="391b2-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="391b2-242">Haga clic en **guardar** en el archivo Web.config de Visual Studio toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="391b2-243">Ejecutar el proyecto de hello localmente y registrar un nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="391b2-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="391b2-244">Ahora, ejecute el nuevo proyecto web localmente haciendo clic en el botón de examinar hello en la depuración.</span><span class="sxs-lookup"><span data-stu-id="391b2-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="391b2-245">En este ejemplo se usa Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="391b2-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="391b2-247">En hello esquina superior derecha de página web de hello predeterminada, elija **registrar** tooregister una nueva cuenta:</span><span class="sxs-lookup"><span data-stu-id="391b2-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="391b2-249">Escriba un nombre de usuario y una contraseña:</span><span class="sxs-lookup"><span data-stu-id="391b2-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="391b2-251">Esto crea automáticamente una base de datos en el servidor local de SQL que contiene la información de pertenencia de hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="391b2-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="391b2-252">Una de las tablas de hello (**dbo. AspNetUsers**) contiene web como Hola que acaba de escribir las credenciales de usuario de aplicación.</span><span class="sxs-lookup"><span data-stu-id="391b2-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="391b2-253">Verá esta tabla más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="391b2-254">Cierre la ventana del explorador Hola de página web de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="391b2-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="391b2-255">Esto detiene la aplicación hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="391b2-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="391b2-256">Ahora está listo para el paso siguiente de hello, que es toopublish Hola aplicación tooAzure y probarlo.</span><span class="sxs-lookup"><span data-stu-id="391b2-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="391b2-257">F.</span><span class="sxs-lookup"><span data-stu-id="391b2-257">F.</span></span> <span data-ttu-id="391b2-258">Publicar tooAzure de aplicación web de Hola y probarlo</span><span class="sxs-lookup"><span data-stu-id="391b2-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="391b2-259">Ahora, podrá publicar su aplicación de servicio de aplicaciones web de aplicación tooyour y, a continuación, probarlo toosee forma de conexión híbrida de Hola que configuró anteriormente que se va tooconnect usa la base de datos de la toohello de aplicación web en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="391b2-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="391b2-260">Publicar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="391b2-260">Publish hello web application</span></span>
1. <span data-ttu-id="391b2-261">Puede descargar el perfil de publicación de hello aplicación de servicio de aplicaciones web en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="391b2-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="391b2-262">En la hoja de hello para la aplicación web, haga clic en **Get perfil de publicación**y, a continuación, guardar el equipo de hello archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="391b2-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Descargar perfil de publicación][PortalDownloadPublishProfile]
   
    <span data-ttu-id="391b2-264">A continuación, importará este archivo en la aplicación web de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="391b2-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="391b2-265">En Visual Studio, haga clic en nombre de proyecto de hello en el Explorador de soluciones y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="391b2-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="391b2-267">Hola **Publicar Web** cuadro de diálogo, en hello **perfil** ficha, elija **importación**.</span><span class="sxs-lookup"><span data-stu-id="391b2-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Importación][HCVSPublishWebDialogImport]
4. <span data-ttu-id="391b2-269">Examinar tooyour descarga perfil de publicación, selecciónelo y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="391b2-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Examinar tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="391b2-271">La información de publicación se importa y se muestra en hello **conexión** ficha del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Haga clic en Publicar.][HCVSClickPublish]
   
    <span data-ttu-id="391b2-273">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="391b2-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="391b2-274">Cuando se completa la publicación, el explorador se inicie y mostrar la aplicación de ASP.NET ya le es familiar, salvo que ahora es activo en la nube de Azure de Hola!</span><span class="sxs-lookup"><span data-stu-id="391b2-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="391b2-275">A continuación, usará su toosee de aplicación web en directo su conexión híbrida en acción.</span><span class="sxs-lookup"><span data-stu-id="391b2-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="391b2-276">Hola de prueba completada la aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="391b2-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="391b2-277">En la parte superior de hello derecha de la página web en Azure, elija **sesión**.</span><span class="sxs-lookup"><span data-stu-id="391b2-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="391b2-279">El servicio de aplicaciones de la aplicación web está ahora conectado a base de datos de pertenencia de la aplicación web tooyour en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="391b2-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="391b2-280">tooverify, inicie sesión con hello mismas credenciales que especificó en hello local de base de datos anterior.</span><span class="sxs-lookup"><span data-stu-id="391b2-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="391b2-282">toofurther probar la conexión híbrida nueva, cierre la sesión en la aplicación web de Azure y registrar como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="391b2-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="391b2-283">Proporcione un nuevo nombre de usuario y contraseña y, a continuación, haga clic en **Registrarse**.</span><span class="sxs-lookup"><span data-stu-id="391b2-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="391b2-285">tooverify que las credenciales del usuario nuevo de Hola se han almacenado en la base de datos local a través de la conexión híbrida, abra SQL Management Studio en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="391b2-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="391b2-286">En el Explorador de objetos, expanda hello **MembershipDB** base de datos y, a continuación, expanda **tablas**.</span><span class="sxs-lookup"><span data-stu-id="391b2-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="391b2-287">Menú contextual hello **dbo. AspNetUsers** pertenencia a la tabla y elija **seleccionar 1000 filas superiores** resultados de tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="391b2-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Ver los resultados de Hola][HCTestSSMSTree]
5. <span data-ttu-id="391b2-289">La tabla de pertenencia local ahora muestra ambas cuentas - Hola uno que creaste localmente y Hola uno que creaste en hello nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="391b2-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="391b2-290">Hola uno que creó en la nube de Hola se ha guardado tooyour base de datos local a través de la característica de conexión híbrida de Azure.</span><span class="sxs-lookup"><span data-stu-id="391b2-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="391b2-292">Ahora ha creado e implementado una aplicación web ASP.NET que utiliza una conexión híbrida entre una aplicación web en hello nube de Azure y una base de datos de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="391b2-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="391b2-293">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="391b2-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="391b2-294">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="391b2-294">See Also</span></span>
[<span data-ttu-id="391b2-295">Introducción a las conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="391b2-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="391b2-296">Josh Twist presenta las conexiones híbridas (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="391b2-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="391b2-297">Introducción a las conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="391b2-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="391b2-298">Servicios de BizTalk: pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="391b2-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="391b2-299">Creación de una nube híbrida del mundo real con una perfecta portabilidad de aplicaciones (vídeo de Channel 9)</span><span class="sxs-lookup"><span data-stu-id="391b2-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="391b2-300">Acceso a recursos locales mediante conexiones híbridas en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="391b2-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="391b2-301">Introducción a la identidad de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="391b2-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
