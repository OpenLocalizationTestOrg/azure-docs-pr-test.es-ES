---
title: aaaCreate un plan en la pila de Azure | Documentos de Microsoft
description: "Como administrador de la nube, cree un plan que permita a los suscriptores aprovisionar máquinas virtuales."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a>Creación de un plan en Azure Stack
Los [planes](azure-stack-key-features.md) son agrupaciones de uno o varios servicios. Como proveedor, puede crear planes de inquilinos de tooyour toooffer. A su vez, los inquilinos suscribirán tooyour ofertas toouse Hola planes y servicios que se incluyen. Este ejemplo muestra cómo toocreate un plan que incluya Hola proveedores de recursos de proceso, red y almacenamiento. Este plan ofrece a los suscriptores Hola capacidad tooprovision las máquinas virtuales.

1. Inicie sesión en toohello portal del Administrador de pila de Azure (https://adminportal.local.azurestack.external). Escriba credenciales de Hola de cuenta de hello que creó durante el paso 5 de hello [ejecutar script de PowerShell de hello](azure-stack-run-powershell-script.md) sección.

2. toocreate un plan y la oferta que los inquilinos pueden suscribirse a, haga clic en **New** > **inquilino ofrece + planes** > **Plan**.

   ![](media/azure-stack-create-plan/image01.png)
3. Hola **nuevo Plan** hoja, rellene **nombre para mostrar** y **nombre del recurso**. Hola nombre para mostrar es el nombre descriptivo del plan de Hola que ven los inquilinos. Hola, administrador solo puede ver Hola nombre del recurso. Su Hola nombre administradores usar toowork con hello plan como un recurso de Azure Resource Manager.

   ![](media/azure-stack-create-plan/image02.png)
4. Crear un nuevo **grupo de recursos**, o seleccione uno existente, como un contenedor para el plan de Hola.

   ![](media/azure-stack-create-plan/image02a.png)
5. Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.

   ![](media/azure-stack-create-plan/image03.png)
6. Haga clic en **cuotas**, haga clic en **almacenamiento de Microsoft (local)**y, a continuación, ya sea Hola seleccione predeterminado de cuota o haga clic en **crear nueva cuota** cuota de hello toocustomize.

   ![](media/azure-stack-create-plan/image04.png)
7. Si va a crear una nueva cuota, escriba un nombre para la cuota de hello > establecer los valores de cuota de hello > haga clic en **Aceptar** > haga clic en nombre de Hola de cuota nueva Hola.

   ![](media/azure-stack-create-plan/image06.png)
8. Haga clic en **Microsoft.Network (local)**y, a continuación, ya sea Hola seleccione predeterminado de cuota o haga clic en **crear nueva cuota** cuota de hello toocustomize.

    ![](media/azure-stack-create-plan/image07.png)
9. Si va a crear una nueva cuota, escriba un nombre para la cuota de hello > establecer los valores de cuota de hello > haga clic en **Aceptar** > haga clic en nombre de Hola de cuota nueva Hola.

    ![](media/azure-stack-create-plan/image08.png)
10. Haga clic en **Microsoft.Compute (local)**y, a continuación, ya sea Hola seleccione predeterminado de cuota o haga clic en **crear nueva cuota** cuota de hello toocustomize.

    ![](media/azure-stack-create-plan/image09.png)
11. Si va a crear una nueva cuota, escriba un nombre para la cuota de hello > establecer los valores de cuota de hello > haga clic en **Aceptar** > haga clic en nombre de Hola de cuota nueva Hola.

    ![](media/azure-stack-create-plan/image10.png)
12. Hola **cuotas** hoja, haga clic en **Aceptar**y, a continuación, en hello **nuevo Plan** hoja, haga clic en **crear** plan de hello toocreate.

    ![](media/azure-stack-create-plan/image11.png)
13. toosee su nuevo plan, haga clic en **todos los recursos**, a continuación, busque el plan de Hola y haga clic en su nombre.

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a>Pasos siguientes
[Creación de una oferta](azure-stack-create-offer.md)
