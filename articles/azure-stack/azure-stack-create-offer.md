---
title: aaaCreate una oferta de pila de Azure | Documentos de Microsoft
description: "Como administrador de la nube, obtenga información acerca de cómo toocreate una oferta para los inquilinos en la pila de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a>Creación de una oferta en Azure Stack
[Ofrece](azure-stack-key-features.md) son grupos de uno o varios planes que toopurchase tootenants presente de proveedores o suscribirse a. Este documento muestra cómo una oferta que incluye hello toocreate [plan que creó](azure-stack-create-plan.md) en el último paso de Hola. Esta oferta proporciona a los suscriptores Hola capacidad tooprovision las máquinas virtuales.

1. Inicie sesión en el portal de administración de Azure pila toohello (https://adminportal.local.azurestack.external) > haga clic en **New** > **inquilino ofrece + planes**  >   **Ofrecer**.

   ![](media/azure-stack-create-offer/image01.png)
2. Hola **ofrecen nuevas** hoja, rellene **nombre para mostrar** y **nombre de recurso**y, a continuación, seleccione un nuevo o existente **grupo de recursos**. Hola nombre para mostrar es el nombre descriptivo de la oferta de Hola y Hola solo información acerca de la oferta de Hola que verán los usuarios de hello cuando se suscriba. Por lo tanto, ser seguro toouse un nombre intuitivo que ayuda a usuario de Hola a entender lo que viene con la oferta de Hola. Hola, administrador solo puede ver Hola nombre del recurso. Su Hola nombre que administradores utilizar toowork con Hola oferta como un recurso de Azure Resource Manager.

   ![](media/azure-stack-create-offer/image01a.png)
3. Haga clic en **Base planes** y, en hello **planear** hoja, planes de hello select que desee tooinclude de la oferta de hello y, a continuación, haga clic en **seleccione**. Haga clic en **crear** oferta de hello toocreate.

   ![](media/azure-stack-create-offer/image02.png)
4. Haga clic en **todos los recursos**, busque la oferta de nuevo, haga clic en nueva oferta de hello, haga clic en **cambio de estado**y, a continuación, haga clic en **público**.

   ![](media/azure-stack-create-offer/image03.png)

Ofertas deben realizarse públicas para la vista completa de los inquilinos tooget Hola al suscribirse. Las ofertas pueden ser:

* **Pública**: tootenants Visible.
* **Privada**: toohello visible solo a los administradores de la nube. Útil al plan de redacción Hola o la oferta, o si desea que Administrador de la nube de hello tooapprove todas las suscripciones.
* **Estado de retiro**: cierra toonew suscriptores. Administrador de la nube de Hello puede utilizar suscripciones futuras tooprevent dado de baja, pero deja intactos los suscriptores actuales.

Cambios toohello oferta no son visibles inmediatamente toohello inquilino. cambios de hello toosee, podría tener nueva suscripción de inicio de sesión/toologout toosee hello en hello "Selector de suscripciones" al crear grupos de recursos y recursos.

> [!NOTE]
>También puede crear ofertas de manera predeterminada, los planes y las cuotas mediante PowerShell, como se explica en hello [archivo Léame del Administrador de servicios de Azure pila](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).
>


## <a name="next-steps"></a>Pasos siguientes
[Suscribirse tooan oferta y, a continuación, aprovisionar una máquina virtual](azure-stack-subscribe-plan-provision-vm.md)
