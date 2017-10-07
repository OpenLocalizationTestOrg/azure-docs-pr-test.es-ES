---
title: Hola aaaDownload Azure SDK para PHP
description: "Obtenga información acerca de cómo toodownload e instalar hello Azure SDK para PHP."
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
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="ae15c-103">Descargar hello Azure SDK para PHP</span><span class="sxs-lookup"><span data-stu-id="ae15c-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="ae15c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ae15c-104">Overview</span></span>
<span data-ttu-id="ae15c-105">Hello Azure SDK para PHP incluye componentes que le permiten toodevelop, implementar y administrar aplicaciones de PHP para Azure.</span><span class="sxs-lookup"><span data-stu-id="ae15c-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="ae15c-106">En concreto, hello Azure SDK para PHP incluye siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="ae15c-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="ae15c-107">**Hola bibliotecas de cliente PHP para Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae15c-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="ae15c-108">Estas bibliotecas de clases proporcionan una interfaz para tener acceso a características de Azure, como los servicios de administración de datos y los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="ae15c-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="ae15c-109">**Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)**.</span><span class="sxs-lookup"><span data-stu-id="ae15c-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="ae15c-110">Este es un conjunto de herramientas que sirve para implementar y administrar servicios de Azure, como Sitios web Azure y Red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae15c-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="ae15c-111">Hola trabajo CLI de Azure en cualquier plataforma, como Mac, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="ae15c-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="ae15c-112">**Azure PowerShell (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="ae15c-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="ae15c-113">Este es un conjunto de cmdlets de PowerShell para implementar y administrar servicios de Azure, como Servicios en la nube y Máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ae15c-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="ae15c-114">**Hola emuladores de Azure (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="ae15c-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="ae15c-115">los emuladores de proceso y almacenamiento de Hello son emuladores locales de servicios en la nube y los servicios de administración de datos que le permiten tootest localmente una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae15c-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="ae15c-116">Hola emuladores de Azure solo se ejecutan en Windows.</span><span class="sxs-lookup"><span data-stu-id="ae15c-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="ae15c-117">Hola las siguientes secciones describen cómo toodownload e instalar Hola componentes descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ae15c-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="ae15c-118">Hello instrucciones de este tema se suponen que tiene [PHP] [ install-php] instalado.</span><span class="sxs-lookup"><span data-stu-id="ae15c-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="ae15c-119">Debe tener PHP 5.5 o bibliotecas de cliente PHP de hello toouse superior para Azure.</span><span class="sxs-lookup"><span data-stu-id="ae15c-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="ae15c-120">Bibliotecas de clientes PHP para Azure</span><span class="sxs-lookup"><span data-stu-id="ae15c-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="ae15c-121">Bibliotecas de cliente de Hello PHP para Azure proporcionan una interfaz para tener acceso a características de Azure, como los servicios de administración de datos y servicios desde cualquier sistema operativo en la nube.</span><span class="sxs-lookup"><span data-stu-id="ae15c-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="ae15c-122">Estas bibliotecas se pueden instalar a través de hello compositor.</span><span class="sxs-lookup"><span data-stu-id="ae15c-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="ae15c-123">Para obtener información acerca de cómo toouse Hola bibliotecas de cliente de PHP para Azure, consulte [cómo tooUse Hola servicio Blob][blob-service], [cómo tooUse Hola servicio tabla] [ table-service] y [cómo tooUse Hola servicio cola][queue-service].</span><span class="sxs-lookup"><span data-stu-id="ae15c-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="ae15c-124">Instalación mediante el compositor</span><span class="sxs-lookup"><span data-stu-id="ae15c-124">Install via Composer</span></span>
1. <span data-ttu-id="ae15c-125">[Instalación de Git][install-git]</span><span class="sxs-lookup"><span data-stu-id="ae15c-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="ae15c-126">En Windows, también necesitará la variable de entorno PATH de tooadd Hola Git tooyour ejecutable.</span><span class="sxs-lookup"><span data-stu-id="ae15c-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="ae15c-127">Cree un archivo denominado **composer.json** en Hola raíz del proyecto y agregue Hola después tooit de código:</span><span class="sxs-lookup"><span data-stu-id="ae15c-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="ae15c-128">Descargue **[composer.phar][composer-phar]** en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ae15c-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="ae15c-129">Abra un símbolo del sistema y ejecute esto en la raíz del proyecto</span><span class="sxs-lookup"><span data-stu-id="ae15c-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="ae15c-130">Azure PowerShell y emuladores de Azure</span><span class="sxs-lookup"><span data-stu-id="ae15c-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="ae15c-131">Azure PowerShell es un conjunto de cmdlets de PowerShell para implementar y administrar servicios de Azure (como Servicios en la nube y Máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="ae15c-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="ae15c-132">Hola emuladores de Azure son emuladores de servicios en la nube y los servicios de administración de datos que le permiten tootest localmente una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae15c-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="ae15c-133">Estos componentes solo son compatibles con Windows.</span><span class="sxs-lookup"><span data-stu-id="ae15c-133">These components are supported Windows only.</span></span>

<span data-ttu-id="ae15c-134">Hola forma recomendada tooinstall PowerShell de Azure y Hola emuladores de Azure es hello toouse [instalador de plataforma Web de Microsoft][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="ae15c-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="ae15c-135">Tenga en cuenta que también puede elegir tooinstall otros componentes de desarrollo, como PHP, SQL Server, Hola Microsoft Drivers para SQL Server para PHP y WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="ae15c-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="ae15c-136">Para obtener información acerca de cómo toouse PowerShell de Azure, consulte [cómo tooUse Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="ae15c-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="ae15c-137">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ae15c-137">Azure CLI</span></span>
<span data-ttu-id="ae15c-138">Hola CLI de Azure es un conjunto de comandos para implementar y administrar servicios de Azure, como sitios Web de Azure y máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae15c-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="ae15c-139">Para obtener información acerca de cómo instalar la CLI de Azure, consulte [Install hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ae15c-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae15c-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae15c-140">Next steps</span></span>
<span data-ttu-id="ae15c-141">Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ae15c-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
