---
title: "Notas de la versión de Azure Data Catalog | Microsoft Docs"
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
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="fcb78-103">Notas de la versión del Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="fcb78-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="fcb78-104">Notas de la versión del 20 de noviembre de 2015 del Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="fcb78-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="fcb78-105">Apertura de orígenes de datos en Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="fcb78-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="fcb78-106">Al usar la opción "Abrir en Power BI Desktop" del portal de **Catálogo de datos de Azure** , es posible que los usuarios se encuentren uno o dos problemas en la aplicación Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="fcb78-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="fcb78-107">Se mostrará un cuadro de diálogo con el título "No se puede abrir el documento"</span><span class="sxs-lookup"><span data-stu-id="fcb78-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="fcb78-108">A continuación, se abre la aplicación Power BI Desktop, pero el archivo parece vacío</span><span class="sxs-lookup"><span data-stu-id="fcb78-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="fcb78-109">Para cada situación, se puede resolver el problema descargando e instalando la versión más reciente de Power BI Desktop de [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="fcb78-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="fcb78-110">Notas de la versión del 13 de noviembre de 2015 del Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="fcb78-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="fcb78-111">Registro y conexión a Teradata</span><span class="sxs-lookup"><span data-stu-id="fcb78-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="fcb78-112">Para conectarse a orígenes de datos de Teradata, los usuarios deben tener instalados los controladores ODBC de Teradata correctos que coinciden con el valor de bits (32 bits o 64 bits) del software que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="fcb78-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="fcb78-113">A partir de esta fecha de lanzamiento de ADC, el [Controlador ODBC de Teradata para Windows (versión 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) más reciente será compatible con Office 2013, pero no con Office 2016.</span><span class="sxs-lookup"><span data-stu-id="fcb78-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="fcb78-114">Notas de la versión del 13 de julio de 2015 del Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="fcb78-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="fcb78-115">Registro y conexión a Oracle Database</span><span class="sxs-lookup"><span data-stu-id="fcb78-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="fcb78-116">Para conectarse a orígenes de datos de Oracle Database, los usuarios deben tener instalados los controladores de Oracle correctos que coinciden con el valor de bits (32 bits o 64 bits) del software que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="fcb78-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="fcb78-117">Al registrar orígenes de datos de Oracle en un equipo con Windows de 32 bits, se usarán controladores de Oracle de 32 bits</span><span class="sxs-lookup"><span data-stu-id="fcb78-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="fcb78-118">Al registrar orígenes de datos de Oracle en un equipo con Windows de 64 bits, se usarán los controladores de Oracle de 64 bits</span><span class="sxs-lookup"><span data-stu-id="fcb78-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="fcb78-119">Para conectarse a orígenes de datos de Oracle mediante Excel en un equipo con la versión de 32 bits de Microsoft Office, incluida en Windows de 64 bits, se usarán los controladores de Oracle de 32 bits</span><span class="sxs-lookup"><span data-stu-id="fcb78-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="fcb78-120">Para conectarse a orígenes de datos de Oracle mediante Excel en un equipo con la versión de 64 bits de Microsoft Office, se usarán los controladores de Oracle de 64 bits</span><span class="sxs-lookup"><span data-stu-id="fcb78-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="fcb78-121">Registro y conexión a SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="fcb78-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="fcb78-122">La compatibilidad con orígenes de datos de SQL Server Reporting Services (SSRS) está actualmente limitada solo a los servidores en modo nativo.</span><span class="sxs-lookup"><span data-stu-id="fcb78-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="fcb78-123">La compatibilidad con SSRS en modo SharePoint se agregará en una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="fcb78-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="fcb78-124">Apertura de recursos de datos en Excel</span><span class="sxs-lookup"><span data-stu-id="fcb78-124">Opening data assets in Excel</span></span>
<span data-ttu-id="fcb78-125">Al abrir recursos de datos en Microsoft Excel desde el portal **Azure Data Catalog**, es posible que a los usuarios se les presente un cuadro de diálogo **Aviso de seguridad de Microsoft Excel**.</span><span class="sxs-lookup"><span data-stu-id="fcb78-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="fcb78-126">Se trata del comportamiento estándar esperado y los usuarios pueden seleccionar **Habilitar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="fcb78-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="fcb78-127">Para obtener más información, vea [Habilitación o deshabilitación de alertas de seguridad sobre vínculos y archivos de sitios web sospechosos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="fcb78-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="fcb78-128">Configuración de proxy y directiva, y registro de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="fcb78-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="fcb78-129">Es posible que los usuarios se encuentren en una situación en la que puedan iniciar sesión en el portal del Catálogo de datos de Azure, pero cuando intenten iniciar sesión en la herramienta de registro de orígenes de datos se encuentren un mensaje de error que les impida iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="fcb78-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="fcb78-130">Hay dos causas posibles para este comportamiento del problema:</span><span class="sxs-lookup"><span data-stu-id="fcb78-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="fcb78-131">**Causa 1: configuración de Servicios de federación de Active Directory** La herramienta de registro de orígenes de datos usa la autenticación de formularios para validar los inicios de sesión de usuario en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcb78-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="fcb78-132">Para iniciar sesión correctamente, la autenticación de formularios debe ser habilitada en la directiva de autenticación global por un administrador de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcb78-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="fcb78-133">En algunas situaciones, es posible que este comportamiento incorrecto ocurra solamente cuando el usuario está en la red de la compañía o solo cuando el usuario se conecta desde fuera de la red de empresa.</span><span class="sxs-lookup"><span data-stu-id="fcb78-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="fcb78-134">La directiva de autenticación global permite habilitar los métodos de autenticación de forma independiente para las conexiones de extranet y de intranet.</span><span class="sxs-lookup"><span data-stu-id="fcb78-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="fcb78-135">Es posible que se produzcan errores de inicio de sesión si no está habilitada la autenticación de formularios para la red desde la que se conecta el usuario.</span><span class="sxs-lookup"><span data-stu-id="fcb78-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="fcb78-136">Para obtener más información, vea [Configuración de directivas de autenticación](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="fcb78-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="fcb78-137">**Causa 2: configuración del proxy de red** Si la red corporativa usa un servidor proxy, es posible que la herramienta de registro no pueda conectarse a Azure Active Directory a través del proxy.</span><span class="sxs-lookup"><span data-stu-id="fcb78-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="fcb78-138">Los usuarios pueden asegurarse de que la herramienta de registro se conecta mediante la edición del archivo de configuración de la herramienta, agregando esta sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="fcb78-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="fcb78-139">Para localizar el archivo RegistrationTool.exe.config, inicie la herramienta de registro y, a continuación, abra la utilidad Administrador de tareas de Windows.</span><span class="sxs-lookup"><span data-stu-id="fcb78-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="fcb78-140">En la pestaña Detalles del Administrador de tareas, haga clic con el botón derecho en RegistrationTool.exe y elija Abrir ubicación de archivo en el menú emergente.</span><span class="sxs-lookup"><span data-stu-id="fcb78-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
