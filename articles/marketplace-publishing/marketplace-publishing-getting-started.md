---
title: "aaaOverview de cómo toocreate e implementar un toohello de oferta de Marketplace | Documentos de Microsoft"
description: "Comprender Hola pasos necesarios toobecome un desarrollador de Microsoft aprobado y crear e implementar una imagen de máquina virtual, la plantilla, el servicio de datos o el servicio de programador en hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Publicar y administrar una oferta de hello Azure Marketplace
En este artículo se proporciona toohelp a los desarrolladores crear, implementar y administrar sus soluciones enumerados en hello Azure Marketplace para otros clientes de Azure y socios toopurchase y uso.

## <a name="marketplace-publishing"></a>Publicación de Marketplace
Como un publicador de Azure, puede distribuir y vender sus soluciones innovadoras o los programadores tooother del servicio, ISV, y los profesionales de TI en Hola Marketplace. A través de hello Marketplace, puede llegar a los clientes que desean tooquickly desarrollan sus aplicaciones basadas en la nube y soluciones para dispositivos móviles. Si la solución está destinado a los usuarios empresariales, puede ser conveniente hello tooconsider [AppSource](http://appsource.microsoft.com) marketplace.


## <a name="supported-types-of-solutions"></a>Tipos de soluciones admitidas
Hola primero que conviene toodo tal y como un publicador es toodefine qué tipo de solución es que ofrece a su empresa. Hola Marketplace admite Hola siguientes tipos de ofertas:

|Tipo de solución|Máquina virtual|Plantilla de solución|
|---|---|---|
|**Definición**|Imágenes preconfiguradas con un sistema operativo completamente instalado y una o varias aplicaciones. Una imagen de máquina virtual proporciona Hola información necesarios toocreate e implementar máquinas virtuales en hello servicio máquinas virtuales de Azure.|Una estructura de datos que puede hacer referencia a uno o más servicios de Azure distintos, incluidos los servicios publicados por otros vendedores. Los suscriptores de Azure pueden usar toodeploy una o más ofertas de forma única y coordinada.|
|**Ejemplo**|Como publicador de Azure, ha creado y validado una máquina virtual con un servicio de base de datos innovador. Otros suscriptores de Azure desea tooprocure e implementación esta máquina virtual en sus entornos de servicio de nube.|Como un publicador de Azure, ha incluido un conjunto de servicios de a través de Azure que facilitan el rápido toodeploy servicios en la nube con equilibrio de carga, mejora la seguridad y alta disponibilidad. Otros suscriptores de Azure pueden ahorrar tiempo si la obtención de la plantilla de solución de Hola que cumpla su objetivo. No tienen toomanually buscar, adquirir, implementar y configurar Hola igual o similares que los servicios de Azure.|

> [!NOTE]
> Algunos pasos se comparten entre los distintos tipos de soluciones de Hola y otras son distintos toohello respectivos tipo de solución. Este artículo proporciona una breve introducción de los pasos de hello necesita toocomplete para cualquier tipo de solución.

## <a name="publish-a-solution"></a>Publicación de una solución
![Nominación, registro y publicación](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Designación de la solución para su aprobación previa
una máquina virtual de toopublish [solución](https://createopportunity.azurewebsites.net) toohello Marketplace, Hola completa Microsoft Azure Certified **solución nominación formato**.

>[!NOTE]
> Si está trabajando con un administrador de cuenta de socio comercial o un administrador de socios comerciales DX, pídale toonominate la solución para el programa de Azure Certified Hola. También puede ir toohello [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) las páginas Web y rellene Hola formulario de la aplicación. Escriba la dirección de correo de Hola de su administrador de cuenta de socios comerciales o administrador de socios comerciales DX Hola **Microsoft patrocinador del contacto** cuadro.

Si se cumplen los criterios de idoneidad de Hola Hola [directivas de participación de Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833) y se aprueba la solicitud, se comienza a trabajar con tooonboard su toohello solución Marketplace.

### <a name="register-your-account-as-a-microsoft-seller"></a>Registrar de la cuenta como vendedor de Microsoft
Registre su cuenta Microsoft como una [cuenta de Microsoft Developer](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Publicación de la solución
toopublish un toohello solución Marketplace, siga estos pasos:
1. Cumplir los requisitos técnicos de Hola.

    a. Cumplir hello [requisitos previos no técnicos](marketplace-publishing-pre-requisites.md).

    b. Cumplir hello [los requisitos previos VM técnicos](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Cumplir hello [requisitos previos de técnica de plantilla de solución](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Cree la oferta.

    a. Cree una oferta de [máquina virtual](marketplace-publishing-vm-image-creation.md).

    b. Cree una oferta de [plantilla de solución](marketplace-publishing-solution-template-creation.md).

3. Cree el [contenido de marketing](marketplace-publishing-push-to-staging.md) de su oferta.

4. Pruebe su oferta en el entorno de ensayo.

    a. Pruebe la oferta de máquina virtual en el [entorno de ensayo](marketplace-publishing-vm-image-test-in-staging.md).

    b. Pruebe la oferta de plantilla de solución en el [entorno de ensayo](marketplace-publishing-solution-template-test-in-staging.md).

5. Implementar la oferta toohello [Marketplace](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Creación y administración de una imagen de máquina virtual
Cree y administre una imagen de máquina virtual mediante estos recursos:
* Creación de una imagen de máquina virtual en el [entorno local](marketplace-publishing-vm-image-creation-on-premise.md).
* Crear una máquina virtual ejecuta [Windows Hola portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Crear una máquina virtual ejecuta [Linux en el portal de Azure hello](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Solución de problemas comunes detectados durante la [creación del VHD](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Administración de la solución
Administrar la solución con la Ayuda de hello recursos siguientes:
* [Leer la Guía de posterior a la producción de hello para la máquina virtual ofrece](marketplace-publishing-vm-image-post-publishing.md)
* [Actualizar los detalles técnicos de Hola de una oferta o una SKU](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Actualizar detalles técnicos de Hola de una oferta o una SKU](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Incorporación de una nueva SKU en una oferta activa](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Cambiar el número de discos de datos de Hola para una SKU enumerada](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Eliminar una oferta enumerada de hello Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [Eliminar una lista de SKU de hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Eliminar versión actual de Hola de una SKU enumerada de hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Revertir Hola enumerar valores de precio tooproduction](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Revertir hello tooproduction valores del modelo de facturación](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Revertir la configuración de visibilidad de Hola de un valor de producción de toohello SKU enumerado](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Cambio del incentivo de revendedores para proveedores de soluciones en la nube](marketplace-publishing-csp-incentive.md)
* [Descripción de los informes de pago](marketplace-publishing-report-payout.md)
* [Obtención de soporte técnico como publicador](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Recursos adicionales
[Configuración de Azure PowerShell](marketplace-publishing-powershell-setup.md)
