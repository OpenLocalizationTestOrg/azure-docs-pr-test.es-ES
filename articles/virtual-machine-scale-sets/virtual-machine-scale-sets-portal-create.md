---
title: "aaaCreate un conjunto de escala de máquinas virtuales usando Hola portal de Azure | Documentos de Microsoft"
description: "Implementación de conjuntos de escalado mediante Azure Portal."
keywords: "conjuntos de escalado de máquinas virtuales"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>¿Cómo toocreate un conjunto de escala de máquinas virtuales con Hola portal de Azure
Este tutorial muestra lo fácil que es toocreate un conjunto de escala de máquinas virtuales en unos pocos minutos, mediante el uso de hello portal de Azure. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Elija la imagen de máquina virtual de Hola de marketplace de Hola
Desde el portal de hello, puede implementar fácilmente una escala establecida con CentOS, CoreOS, Debian, abra Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server o imágenes de Windows Server.

En primer lugar, navegue toohello [portal de Azure](https://portal.azure.com) en un explorador web. Haga clic en `New`, busque `scale set`y, a continuación, seleccione hello `Virtual machine scale set` entrada:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Crear conjunto de escalas de Hola
Ahora puede utilizar la configuración predeterminada de Hola y crear rápidamente el conjunto de escalas de Hola.

* En hello `Basics` hoja, escriba un nombre para el conjunto de escalas de Hola. Este nombre se convierte en base Hola de hello FQDN del equilibrador de carga de hello delante de conjunto de escalas de hello, así que asegúrese de hello nombre es único a través de Azure todos.
* Seleccione su tipo preferido de sistema operativo, escriba el nombre de usuario que quiera y seleccione el tipo de autenticación que desee. Si elige una contraseña, debe ser como mínimo 12 caracteres de longitud y satisfacer tres de hello cuatro requisitos de complejidad: caracteres de una minúscula, una letra mayúscula, un número y un carácter especial. Obtenga más información acerca de los [requisitos de usuario y la contraseña](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Si elige `SSH public key`, puede pegar tooonly seguro en la clave pública, no su clave privada:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Elija si quiere que escala de hello toolimit configurada tooa grupo de selección de ubicación único o si deben abarcar varios grupos de selección de ubicación. Permitir que el conjunto de escalado de hello toospan grupos de selección de ubicación permite escala establece más de 100 máquinas virtuales de capacidad (arriba too1, 000) con ciertas limitaciones. Para obtener más información, consulte [esta documentación](./virtual-machine-scale-sets-placement-groups.md).
* Escriba el nombre del grupo de recursos y la ubicación que quiera y haga clic en `OK`.
* En hello `Virtual machine scale set service settings` hoja: escriba la etiqueta de nombre de dominio que desee (base de Hola de hello FQDN para el equilibrador de carga de hello delante de conjunto de escalas de hello). Esta etiqueta debe ser única en todo Azure.
* Elija la imagen de disco del sistema operativo que desee, el recuento de instancias y el tamaño de máquina.
* Elija el tipo de disco que desee: administrado o no administrado. Para obtener más información, consulte [esta documentación](./virtual-machine-scale-sets-managed-disks.md). Si opta por conjunto de escalas de hello toohave abarcar varios grupos de selección de ubicación, esta opción no estará disponible porque se requiere para grupos de selección de ubicación de escala conjuntos toospan disco administrado.
* Habilite o deshabilite el escalado automático y, si lo habilita, configúrelo:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* En hello `Summary` hoja, cuando se realiza la validación, haga clic en `OK` conjunto de escalado de hello toostart de implementación.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Conectar tooa VM en el conjunto de escalas de Hola
Si ha elegido toolimit su escala establezca tooa grupo de selección de ubicación única y conjunto de escalas de Hola se implementa con NAT configurado reglas toolet conectar escala toohello establecer fácilmente (si no es así, Establece tooconnect toohello máquinas en escala de hello, probablemente necesitará toocreate un jumpbox Hola misma red virtual como conjunto de escalas de hello). toosee, navegue toohello `Inbound NAT Rules` ficha Hola de equilibrador de carga para el conjunto de escalas de hello:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Puede conectarse tooeach conjunto de máquinas virtuales en la escala de hello utilizando estas reglas NAT. Por ejemplo, para un conjunto de escala de Windows, si hay una regla NAT en el puerto entrante 50000, puede conectarse toothat máquina a través de RDP en `<load-balancer-ip-address>:50000`. Para un conjunto de escalas de Linux, se conectará con el comando de hello `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Pasos siguientes
Para obtener documentación sobre cómo se establece toodeploy escala de hello CLI, consulte [esta documentación](virtual-machine-scale-sets-cli-quick-create.md).

Para obtener documentación sobre cómo se establece toodeploy escala desde PowerShell, consulte [esta documentación](virtual-machine-scale-sets-windows-create.md).

Para obtener documentación sobre cómo se establece toodeploy escala desde Visual Studio, vea [esta documentación](virtual-machine-scale-sets-vs-create.md).

Para obtener documentación general, visite hello [página de información general de documentación de conjuntos de escalas de](virtual-machine-scale-sets-overview.md).

Para obtener información general, consulte hello [página de aterrizaje principal para conjuntos de escalas de](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

