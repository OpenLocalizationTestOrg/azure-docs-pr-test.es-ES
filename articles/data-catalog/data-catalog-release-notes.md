---
title: "notas de la versión de aaaAzure el catálogo de datos | Documentos de Microsoft"
description: "Las notas de la versión del Catálogo de datos de Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="9e9d6-103">Notas de la versión del Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="9e9d6-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="9e9d6-104">Notas de versión de 20 de noviembre de 2015 Hola del catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="9e9d6-104">Notes for hello November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="9e9d6-105">Apertura de orígenes de datos en Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9e9d6-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="9e9d6-106">Cuando se usa la opción de "Abrir en Power BI Desktop" hello de hello **el catálogo de datos** portal, los usuarios pueden encontrarse alguno de estos dos problemas en hello aplicación de Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="9e9d6-106">When using hello "Open in Power BI Desktop" option from hello **Azure Data Catalog** portal, users may encounter one of two problems in hello Power BI Desktop application:</span></span>

* <span data-ttu-id="9e9d6-107">Se muestra un cuadro de diálogo con el título de hello "No se puede tooOpen documento"</span><span class="sxs-lookup"><span data-stu-id="9e9d6-107">A dialog box with hello title "Unable tooOpen Document" is displayed</span></span>
* <span data-ttu-id="9e9d6-108">se abre Hola aplicación de Power BI Desktop, pero archivo hello aparece toobe vacía</span><span class="sxs-lookup"><span data-stu-id="9e9d6-108">hello Power BI Desktop application opens, but hello file appears toobe empty</span></span>

<span data-ttu-id="9e9d6-109">En cada situación, se puede resolver el problema de hello, descargue e instale la versión más reciente de Hola de Power BI Desktop desde [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="9e9d6-109">For each situation, hello problem can be resolved by downloading and installing hello latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="9e9d6-110">Notas de versión de 13 de noviembre de 2015 Hola del catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="9e9d6-110">Notes for hello November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-tooteradata"></a><span data-ttu-id="9e9d6-111">Registrar y conectar tooTeradata</span><span class="sxs-lookup"><span data-stu-id="9e9d6-111">Registering and connecting tooTeradata</span></span>
<span data-ttu-id="9e9d6-112">Al conectarse a orígenes de datos de tooTeradata usuarios deben tener instalado el controlador ODBC Teradata correcto de Hola que coinciden con los bits de hello (32 bits o 64 bits) del software de Hola que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-112">When connecting tooTeradata data sources users must have installed hello correct Teradata ODBC driver that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

<span data-ttu-id="9e9d6-113">A partir de este ADC, fecha de lanzamiento, Hola más reciente [el controlador ODBC de Teradata para windows (versión 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) es compatible con Office 2013, pero no con Office 2016.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-113">As of this ADC release date, hello most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="9e9d6-114">Notas de versión de 13 de julio de 2015 Hola del catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="9e9d6-114">Notes for hello July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-toooracle-database"></a><span data-ttu-id="9e9d6-115">Registrar y conectar tooOracle base de datos</span><span class="sxs-lookup"><span data-stu-id="9e9d6-115">Registering and connecting tooOracle Database</span></span>
<span data-ttu-id="9e9d6-116">Al conectar a los usuarios en orígenes de datos de base de datos en tooOracle debe haber instalado controladores Oracle correspondientes Hola que coinciden con los bits de hello (32 bits o 64 bits) del software de Hola que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-116">When connecting tooOracle Database data sources users must have installed hello correct Oracle drivers that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

* <span data-ttu-id="9e9d6-117">Al registrar los orígenes de datos de Oracle en un equipo que ejecuta Windows de 32 bits, se usará controladores de Oracle de 32 bits de Hola</span><span class="sxs-lookup"><span data-stu-id="9e9d6-117">When registering Oracle data sources on a computer running 32-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="9e9d6-118">Al registrar los orígenes de datos de Oracle en un equipo que ejecuta Windows de 64 bits, se usará controladores de Oracle de 64 bits de Hola</span><span class="sxs-lookup"><span data-stu-id="9e9d6-118">When registering Oracle data sources on a computer running 64-bit Windows, hello 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="9e9d6-119">Al conectarse a orígenes de datos de tooOracle usa Excel en un equipo que ejecuta la versión de 32 bits de Hola de Microsoft Office, incluido en Windows de 64 bits, controladores de Oracle de 32 bits de Hola se utilizará</span><span class="sxs-lookup"><span data-stu-id="9e9d6-119">When connecting tooOracle data sources using Excel on a computer running hello 32-bit version of Microsoft Office, including on 64-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="9e9d6-120">Al conectarse a orígenes de datos de tooOracle usa Excel en un equipo que ejecuta la versión de 64 bits de Hola de Microsoft Office, se usará controladores de Oracle de 64 bits de Hola</span><span class="sxs-lookup"><span data-stu-id="9e9d6-120">When connecting tooOracle data sources using Excel on a computer running hello 64-bit version of Microsoft Office, hello 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-toosql-server-reporting-services"></a><span data-ttu-id="9e9d6-121">Registrar y conectar tooSQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="9e9d6-121">Registering and connecting tooSQL Server Reporting Services</span></span>
<span data-ttu-id="9e9d6-122">Compatibilidad con orígenes de datos de SQL Server Reporting Services (SSRS) está actualmente hay una limitación tooNative sólo los servidores de modo.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited tooNative Mode servers only.</span></span> <span data-ttu-id="9e9d6-123">La compatibilidad con SSRS en modo SharePoint se agregará en una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="9e9d6-124">Apertura de recursos de datos en Excel</span><span class="sxs-lookup"><span data-stu-id="9e9d6-124">Opening data assets in Excel</span></span>
<span data-ttu-id="9e9d6-125">Al abrir los activos de datos en Microsoft Excel de hello **el catálogo de datos** portal, los usuarios que se le pida con un **aviso de seguridad de Microsoft Excel** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-125">When opening data assets in Microsoft Excel from hello **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="9e9d6-126">Se trata de estándar, pueden seleccionar el comportamiento esperado y los usuarios **habilitar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-126">This is standard, expected behavior, and users can select **Enable** toocontinue.</span></span>

<span data-ttu-id="9e9d6-127">Para obtener más información, vea [Habilitación o deshabilitación de alertas de seguridad sobre vínculos y archivos de sitios web sospechosos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="9e9d6-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="9e9d6-128">Configuración de proxy y directiva, y registro de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="9e9d6-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="9e9d6-129">Los usuarios pueden encontrarse en una situación donde poder iniciar sesión en el portal del catálogo de datos de Azure de toohello, pero cuando intenten toolog en la herramienta de registro del origen de datos de toohello que aparecen un mensaje de error que impide que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-129">Users may encounter a situation where they can log on toohello Azure Data Catalog portal, but when they attempt toolog on toohello data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="9e9d6-130">Hay dos causas posibles para este comportamiento del problema:</span><span class="sxs-lookup"><span data-stu-id="9e9d6-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="9e9d6-131">**Causa 1: Configuración de servicios de federación de Active Directory** herramienta de registro de origen de datos de hello usa inicios de sesión de autenticación de formularios toovalidate usuario en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-131">**Cause 1: Active Directory Federation Services configuration** hello data source registration tool uses Forms Authentication toovalidate user logons against Active Directory.</span></span> <span data-ttu-id="9e9d6-132">Para iniciar sesión correctamente, la autenticación de formularios debe habilitarse en hello directiva de autenticación Global por un administrador de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-132">For successful logon, Forms Authentication must be enabled in hello Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="9e9d6-133">En algunas situaciones, este error puede ocurrir sólo cuando el usuario de hello en red de empresa de hello, o solo cuando Hola usuario se conecta desde la red de empresa de hello exterior.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-133">In some situations, this error behavior may occur only when hello user is on hello company network, or only when hello user is connecting from outside hello company network.</span></span> <span data-ttu-id="9e9d6-134">Hola directiva de autenticación Global permite toobe de métodos de autenticación habilitado por separado para la intranet y las conexiones de extranet.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-134">hello Global Authentication Policy allows authentication methods toobe enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="9e9d6-135">Si la autenticación de formularios no está habilitada para la red de Hola desde qué Hola usuario se conecta, pueden producirse errores de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-135">Logon errors may occur if Forms Authentication is not enabled for hello network from which hello user is connecting.</span></span>

<span data-ttu-id="9e9d6-136">Para obtener más información, vea [Configuración de directivas de autenticación](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e9d6-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="9e9d6-137">**Causa 2: Configuración de proxy de red** si red corporativa de hello usa un servidor proxy, la herramienta de registro de hello puede no ser capaz de tooconnect tooAzure Active Directory a través de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-137">**Cause 2: Network proxy configuration** If hello corporate network uses a proxy server, hello registration tool may not be able tooconnect tooAzure Active Directory through hello proxy.</span></span> <span data-ttu-id="9e9d6-138">Los usuarios pueden asegurarse de esa herramienta de registro de hello editando el archivo de configuración de la herramienta de hello, agregar este archivo de toohello de sección:</span><span class="sxs-lookup"><span data-stu-id="9e9d6-138">Users can ensure that hello registration tool by editing hello tool’s configuration file, adding this section toohello file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="9e9d6-139">archivo de RegistrationTool.exe.config de toolocate hello, inicie la herramienta de registro de hello y, a continuación, abra la utilidad de administrador de tareas de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-139">toolocate hello RegistrationTool.exe.config file, launch hello registration tool, and then open hello Windows Task Manager utility.</span></span> <span data-ttu-id="9e9d6-140">En la ficha de detalles de hello en el Administrador de tareas, haga doble clic en RegistrationTool.exe y elija Abrir ubicación del archivo desde el menú emergente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e9d6-140">On hello Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from hello pop-up menu.</span></span>
