---
title: Descarga del SDK de Azure para PHP
description: "Obtenga información acerca de cómo descargar e instalar el SDK de Azure para PHP."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="57c53-103">Descarga del SDK de Azure para PHP</span><span class="sxs-lookup"><span data-stu-id="57c53-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="57c53-104">Información general</span><span class="sxs-lookup"><span data-stu-id="57c53-104">Overview</span></span>
<span data-ttu-id="57c53-105">El SDK de Azure para PHP incluye componentes que le permiten desarrollar, implementar y administrar aplicaciones PHP para Azure.</span><span class="sxs-lookup"><span data-stu-id="57c53-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="57c53-106">Específicamente, el SDK de Azure para PHP incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="57c53-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="57c53-107">**Las bibliotecas de clientes PHP para Azure**.</span><span class="sxs-lookup"><span data-stu-id="57c53-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="57c53-108">Estas bibliotecas de clases proporcionan una interfaz para tener acceso a características de Azure, como los servicios de administración de datos y los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="57c53-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="57c53-109">**La interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLIC de Azure)**.</span><span class="sxs-lookup"><span data-stu-id="57c53-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="57c53-110">Este es un conjunto de herramientas que sirve para implementar y administrar servicios de Azure, como Sitios web Azure y Red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="57c53-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="57c53-111">La interfaz de la línea de comandos de Azure funciona en cualquier plataforma, incluidas las plataformas Mac, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="57c53-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="57c53-112">**Azure PowerShell (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="57c53-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="57c53-113">Este es un conjunto de cmdlets de PowerShell para implementar y administrar servicios de Azure, como Servicios en la nube y Máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="57c53-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="57c53-114">**Los emuladores de Azure (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="57c53-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="57c53-115">Los emuladores de proceso y almacenamiento son emuladores locales de los servicios en la nube y los servicios de administración de datos que le permiten probar localmente una aplicación.</span><span class="sxs-lookup"><span data-stu-id="57c53-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="57c53-116">Los emuladores de Azure solo se ejecutan en Windows.</span><span class="sxs-lookup"><span data-stu-id="57c53-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="57c53-117">Las secciones que vienen a continuación describen cómo descargar e instalar los componentes descritos.</span><span class="sxs-lookup"><span data-stu-id="57c53-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="57c53-118">En las instrucciones de este tema se da por hecho que tiene [PHP][install-php] instalado.</span><span class="sxs-lookup"><span data-stu-id="57c53-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="57c53-119">Debe tener instalado PHP 5.5 o superior con el fin de utilizar las bibliotecas de clientes PHP para Azure.</span><span class="sxs-lookup"><span data-stu-id="57c53-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="57c53-120">Bibliotecas de clientes PHP para Azure</span><span class="sxs-lookup"><span data-stu-id="57c53-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="57c53-121">Las bibliotecas de clientes PHP para Azure proporcionan una interfaz para tener acceso a características de Azure, como los servicios de administración de datos y los servicios en la nube, desde cualquier sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="57c53-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="57c53-122">Estas bibliotecas se pueden instalar mediante el Compositor.</span><span class="sxs-lookup"><span data-stu-id="57c53-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="57c53-123">Si desea obtener información sobre el uso de las bibliotecas de clientes PHP para Azure, consulte [Uso del servicio BLOB][blob-service], [Uso del servicio Tabla][table-service] y [Uso del servicio Cola][queue-service].</span><span class="sxs-lookup"><span data-stu-id="57c53-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="57c53-124">Instalación mediante el compositor</span><span class="sxs-lookup"><span data-stu-id="57c53-124">Install via Composer</span></span>
1. <span data-ttu-id="57c53-125">[Instalación de Git][install-git]</span><span class="sxs-lookup"><span data-stu-id="57c53-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="57c53-126">En Windows, también tendrá que agregar el archivo ejecutable Git a la variable de entorno PATH.</span><span class="sxs-lookup"><span data-stu-id="57c53-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="57c53-127">Cree un archivo con el nombre **composer.json** en la raíz del proyecto y agréguele el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="57c53-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="57c53-128">Descargue **[composer.phar][composer-phar]** en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="57c53-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="57c53-129">Abra un símbolo del sistema y ejecute esto en la raíz del proyecto</span><span class="sxs-lookup"><span data-stu-id="57c53-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="57c53-130">Azure PowerShell y emuladores de Azure</span><span class="sxs-lookup"><span data-stu-id="57c53-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="57c53-131">Azure PowerShell es un conjunto de cmdlets de PowerShell para implementar y administrar servicios de Azure (como Servicios en la nube y Máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="57c53-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="57c53-132">Los emuladores de Azure son emuladores de servicios en la nube y servicios de administración de datos que le permiten probar localmente una aplicación.</span><span class="sxs-lookup"><span data-stu-id="57c53-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="57c53-133">Estos componentes solo son compatibles con Windows.</span><span class="sxs-lookup"><span data-stu-id="57c53-133">These components are supported Windows only.</span></span>

<span data-ttu-id="57c53-134">La manera recomendada de instalar Azure PowerShell y los emuladores de Azure es utilizar el [instalador de plataforma web de Microsoft][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="57c53-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="57c53-135">Observe que también puede elegir instalar otros componentes de desarrollo, como PHP, SQL Server, los controladores de Microsoft para SQL Server para PHP y WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="57c53-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="57c53-136">Para obtener más información sobre el uso de Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="57c53-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="57c53-137">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="57c53-137">Azure CLI</span></span>
<span data-ttu-id="57c53-138">La interfaz de la línea de comandos de Azure es un conjunto de herramientas que sirve para implementar y administrar servicios de Azure, como Sitios web Azure y Red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="57c53-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="57c53-139">Para obtener información acerca de cómo instalar la CLI de Azure, consulte [Instalar la CLI de Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="57c53-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="57c53-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57c53-140">Next steps</span></span>
<span data-ttu-id="57c53-141">Para obtener más información, consulte el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="57c53-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
