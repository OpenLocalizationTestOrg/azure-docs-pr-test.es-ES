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
# <a name="download-hello-azure-sdk-for-php"></a>Descargar hello Azure SDK para PHP
## <a name="overview"></a>Información general
Hello Azure SDK para PHP incluye componentes que le permiten toodevelop, implementar y administrar aplicaciones de PHP para Azure. En concreto, hello Azure SDK para PHP incluye siguiente de hello:

* **Hola bibliotecas de cliente PHP para Azure**. Estas bibliotecas de clases proporcionan una interfaz para tener acceso a características de Azure, como los servicios de administración de datos y los servicios en la nube.  
* **Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)**. Este es un conjunto de herramientas que sirve para implementar y administrar servicios de Azure, como Sitios web Azure y Red virtual de Azure. Hola trabajo CLI de Azure en cualquier plataforma, como Mac, Linux y Windows.
* **Azure PowerShell (solo Windows)**. Este es un conjunto de cmdlets de PowerShell para implementar y administrar servicios de Azure, como Servicios en la nube y Máquinas virtuales.
* **Hola emuladores de Azure (solo Windows)**. los emuladores de proceso y almacenamiento de Hello son emuladores locales de servicios en la nube y los servicios de administración de datos que le permiten tootest localmente una aplicación. Hola emuladores de Azure solo se ejecutan en Windows.

Hola las siguientes secciones describen cómo toodownload e instalar Hola componentes descritos anteriormente.

Hello instrucciones de este tema se suponen que tiene [PHP] [ install-php] instalado.

> [!NOTE]
> Debe tener PHP 5.5 o bibliotecas de cliente PHP de hello toouse superior para Azure.
> 
> 

## <a name="php-client-libraries-for-azure"></a>Bibliotecas de clientes PHP para Azure
Bibliotecas de cliente de Hello PHP para Azure proporcionan una interfaz para tener acceso a características de Azure, como los servicios de administración de datos y servicios desde cualquier sistema operativo en la nube. Estas bibliotecas se pueden instalar a través de hello compositor.

Para obtener información acerca de cómo toouse Hola bibliotecas de cliente de PHP para Azure, consulte [cómo tooUse Hola servicio Blob][blob-service], [cómo tooUse Hola servicio tabla] [ table-service] y [cómo tooUse Hola servicio cola][queue-service].

### <a name="install-via-composer"></a>Instalación mediante el compositor
1. [Instalación de Git][install-git]

    > [AZURE.NOTE] En Windows, también necesitará la variable de entorno PATH de tooadd Hola Git tooyour ejecutable.

1. Cree un archivo denominado **composer.json** en Hola raíz del proyecto y agregue Hola después tooit de código:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Descargue **[composer.phar][composer-phar]** en la raíz del proyecto.
3. Abra un símbolo del sistema y ejecute esto en la raíz del proyecto
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell y emuladores de Azure
Azure PowerShell es un conjunto de cmdlets de PowerShell para implementar y administrar servicios de Azure (como Servicios en la nube y Máquinas virtuales). Hola emuladores de Azure son emuladores de servicios en la nube y los servicios de administración de datos que le permiten tootest localmente una aplicación. Estos componentes solo son compatibles con Windows.

Hola forma recomendada tooinstall PowerShell de Azure y Hola emuladores de Azure es hello toouse [instalador de plataforma Web de Microsoft][download-wpi]. Tenga en cuenta que también puede elegir tooinstall otros componentes de desarrollo, como PHP, SQL Server, Hola Microsoft Drivers para SQL Server para PHP y WebMatrix.

Para obtener información acerca de cómo toouse PowerShell de Azure, consulte [cómo tooUse Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>CLI de Azure
Hola CLI de Azure es un conjunto de comandos para implementar y administrar servicios de Azure, como sitios Web de Azure y máquinas virtuales de Azure. Para obtener información acerca de cómo instalar la CLI de Azure, consulte [Install hello Azure CLI](cli-install-nodejs.md).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).

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
