---
title: "imágenes de cliente de Windows aaaUse en Azure | Documentos de Microsoft"
description: "¿Cómo toouse suscripción de Visual Studio beneficios toodeploy Windows 7, Windows 8 o Windows 10 en Azure para escenarios de desarrollo/pruebas"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Uso del cliente Windows en Azure para escenarios de desarrollo y pruebas
Puede usar Windows 7, Windows 8 o Windows 10 en Azure para escenarios de desarrollo y pruebas siempre que tenga una suscripción adecuada a Visual Studio (anteriormente MSDN). En este artículo se describe los requisitos de elegibilidad de Hola para ejecutar el cliente de Windows en Azure y el uso de hello imágenes de la Galería de Azure.

## <a name="subscription-eligibility"></a>Idoneidad de la suscripción
Los suscriptores activos de Visual Studio (es decir, las personas que adquirieron una licencia de suscripción de Visual Studio) pueden usar el cliente Windows para desarrollo y pruebas. El cliente Windows se puede usar en su propio hardware y en máquinas virtuales de Azure que se ejecutan en cualquier tipo de suscripción de Azure. Cliente de Windows no puede ser implementado tooor emplea en Azure para su uso en producción normal, o que utilizan los usuarios que no son suscriptores activos de Visual Studio.

Para su comodidad, hemos realizado determinadas imágenes de Windows 10 disponibles desde galería de Azure de hello en [ofrece apto para desarrollo y pruebas](#eligible-offers). Visual Studio los suscriptores dentro de cualquier tipo de oferta pueden también [adecuadamente preparar y crear](prepare-for-upload-vhd-image.md) una imagen de Windows 7, Windows 8 o Windows 10 de 64 bits y, a continuación, [cargar tooAzure](upload-generalized-managed.md). uso de Hello sigue siendo toodev/prueba limitada por los suscriptores activos de Visual Studio.

## <a name="eligible-offers"></a>Ofertas a las que se puede tener acceso
Hola después Hola de detalles de tabla ofrece identificadores que son apto toodeploy Windows 10 a través de hello Galería de Azure. imágenes de Hello Windows 10 solo están toohello visible después de ofertas. Los suscriptores de Visual Studio que necesita toorun cliente de Windows en un tipo de otra oferta deberá demasiado[adecuadamente preparar y crear](prepare-for-upload-vhd-image.md) una imagen de Windows 7, Windows 8 o Windows 10 de 64 bits y [, a continuación, cargar tooAzure](upload-generalized-managed.md).

| Nombre de la oferta | Número de la oferta | Imágenes de cliente disponibles |
|:--- |:---:|:---:|
| [Desarrollo/pruebas - Pago por uso](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Suscriptores de Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Suscriptores de Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Suscriptores de Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium con MSDN (ventaja)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Suscriptores de Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Suscriptores de Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Desarrollo/pruebas - Enterprise](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Compruebe la suscripción a Azure
Si no conoce el identificador de la oferta, puede obtenerla a través de hello portal de Azure en una de estas dos maneras:  

- En la hoja de "Suscripciones" hello:

  ![Detalles de Id. de la oferta de hello portal de Azure](./media/client-images/offer-id-azure-portal.png) 

- O bien, haga clic en **Facturación** y, a continuación, haga clic en el identificador de suscripción. Identificador de la oferta de Hello aparece en la hoja de facturación de Hola.

También puede ver el identificador de la oferta de Hola de hello [ficha "Suscripciones"](http://account.windowsazure.com/Subscriptions) hello Azure del portal de cuenta:

![Detalles de Id. de la oferta desde el portal de la cuenta de Azure de Hola](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Pasos siguientes
Ahora puede implementar las máquinas virtuales con [PowerShell](quick-create-powershell.md), [plantillas de Resource Manager](ps-template.md) o [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

