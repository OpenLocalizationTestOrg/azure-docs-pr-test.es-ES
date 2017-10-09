---
title: "aaaCreate una prueba de la máquina virtual en la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprovision una prueba de la máquina virtual en la pila de Azure como un operador en la nube."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a>Creación de una máquina virtual en Azure Stack
Como un operador en la nube, puede crear un toovalidate de máquina virtual de prueba de la implementación de la pila de Azure.

> [!NOTE]
> Antes de poder aprovisionar máquinas virtuales, debe [agregar marketplace de pila de Azure de hello evaluación de Windows Server 2016 imagen toohello](azure-stack-add-default-image.md).
> 
> 

## <a name="create-a-virtual-machine"></a>de una máquina virtual
1. En el host del Kit de desarrollo de pila de Azure de hello, [iniciar sesión en](azure-stack-connect-azure-stack.md) toohello portal del administrador (`https://adminportal.local.azurestack.external`) y, a continuación, haga clic en **New** > **proceso**  >  **Datacenter de Windows Server 2016 Eval** > **crear**.  
2. Hola **Fundamentos** hoja, escriba un **nombre**, **nombre de usuario**, y **contraseña**. Elija una **suscripción**. Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.  
3. Hola **elegir un tamaño de** hoja, haga clic en **estándar A1**y, a continuación, haga clic en **seleccione**.  
4. Hola **configuración** hoja, acepte los valores predeterminados de Hola y haga clic en **Aceptar**
5. Hola **resumen** hoja, haga clic en **Aceptar** máquina virtual de toocreate Hola.  
6. toosee la nueva máquina virtual, haga clic en **todos los recursos**, a continuación, busque la máquina virtual de Hola y haga clic en su nombre.
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a>Pasos siguientes
[Uso de portales de administrador y usuario de hello en la pila de Azure](azure-stack-manage-portals.md)
