---
title: "los usuarios de aaaMake máquinas virtuales disponibles tooyour pila de Azure | Documentos de Microsoft"
description: "Máquinas virtuales de tutorial toomake disponibles en la pila de Azure"
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a>Hacer tooyour disponibles de máquinas virtuales que los usuarios de la pila de Azure
Como administrador de la nube de una pila de Azure, puede crear ofertas que se pueden suscribir los usuarios (en ocasiones denominado tooas inquilinos). Con su suscripción, los usuarios podrán consumir servicios de Azure Stack.

Este artículo muestra cómo toocreate una oferta y, a continuación, vuelva a probarlo. Para pruebas de hello, se inicie sesión en el portal de toohello como un usuario, suscribirse toohello oferta y, a continuación, crear una máquina virtual mediante suscripción Hola.

Lo qué aprenderá:

> [!div class="checklist"]
> * Creación de una oferta
> * Añadir una imagen
> * Oferta de prueba Hola


En la pila de Azure, servicios se entregan toousers mediante planes, ofertas y suscripciones. Los usuarios pueden suscribirse toomultiple ofertas. Las ofertas pueden tener uno o varios planes, y los planes pueden tener uno o varios servicios.

![Planes, ofertas y suscripciones](media/azure-stack-key-features/image4.png)

más información, consulte toolearn [principales características y conceptos de Azure pila](azure-stack-key-features.md).

## <a name="create-an-offer"></a>Creación de una oferta

Ahora puede preparar todo para los usuarios. Cuando se inicia el proceso de hello, es la primera oferta de hello toocreate solicitadas, a continuación, un plan y, finalmente, las cuotas.

3. **Creación de una oferta**

   Ofertas son grupos de uno o varios planes que toopurchase toousers presente de proveedores o suscriben a.

   a. [Inicie sesión en](azure-stack-connect-azure-stack.md) toohello portal como un administrador de la nube y, a continuación, haga clic en **New** > **inquilino ofrece + planes** > **ofrecen**.
   ![Nueva oferta](media/azure-stack-tutorial-tenant-vm/image01.png)

   b. Hola **ofrecen nuevas** sección, rellene **nombre para mostrar** y **nombre de recurso**y, a continuación, seleccione un nuevo o existente **grupo de recursos**. Hola nombre para mostrar es el nombre descriptivo de la oferta de Hola. Operador en la nube de hello sólo puede ver Hola nombre del recurso. Su Hola nombre que administradores utilizar toowork con Hola oferta como un recurso de Azure Resource Manager.

   ![Nombre para mostrar](media/azure-stack-tutorial-tenant-vm/image02.png)

   c. Haga clic en **Base planes**y en hello **Plan** sección, haga clic en **agregar** tooadd una nueva oferta de toohello de plan.

   ![Agregar un plan](media/azure-stack-tutorial-tenant-vm/image03.png)

   d. Hola **nuevo Plan** sección, rellene **nombre para mostrar** y **nombre del recurso**. Hola nombre para mostrar es el nombre descriptivo del plan de Hola que ven los usuarios. Operador en la nube de hello sólo puede ver Hola nombre del recurso. Su Hola nombre operadores en la nube usar toowork con hello plan como un recurso de Azure Resource Manager.

   ![Nombre para mostrar del plan](media/azure-stack-tutorial-tenant-vm/image04.png)

   e. Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.

   ![Servicios del plan](media/azure-stack-tutorial-tenant-vm/image05.png)

   f. Haga clic en **cuotas**y, a continuación, seleccione primer servicio de hello para el que desea toocreate una cuota. Para una cuota de IaaS, siga estos pasos para los servicios de proceso, red y almacenamiento de Hola.

   En este ejemplo, primero se crea una cuota para el servicio de proceso de Hola. En la lista del espacio de nombres de hello, seleccione hello **Microsoft.Compute** espacio de nombres y, a continuación, haga clic en **crear nueva cuota**.
   
   ![Crear nueva cuota](media/azure-stack-tutorial-tenant-vm/image06.png)

   g. En hello **Crear cuota** sección, escriba un nombre para la cuota de Hola y establezca Hola parámetros que desee para la cuota de Hola y haga clic en **Aceptar**.

   ![Nombre de cuota](media/azure-stack-tutorial-tenant-vm/image07.png)

   h. Ahora, para **Microsoft.Compute**, seleccione cuota Hola que ha creado.

   ![Seleccione la cuota](media/azure-stack-tutorial-tenant-vm/image08.png)

   Repita estos pasos para los servicios de red y almacenamiento de hello y, a continuación, haga clic en **Aceptar** en hello **cuotas** sección.

   i. Haga clic en **Aceptar** en hello **nuevo plan** sección.

   j. En hello **Plan** sección, seleccione Nuevo plan de Hola y haga clic en **seleccione**.

   k. En hello **oferta nueva** sección, haga clic en **crear**. Verá una notificación cuando se ha creado la oferta de Hola.

   l. En el menú del panel hello, haga clic en **ofrece** y, a continuación, haga clic en oferta Hola que creó.

   m. Haga clic en **Cambiar estado** y, a continuación, haga clic en **Público**.

   ![Estado público](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a>Añadir una imagen

Antes de poder aprovisionar máquinas virtuales, debe agregar un marketplace de imagen toohello pila de Azure. Puede agregar imagen de Hola de su elección, incluidas las imágenes de Linux, de hello Azure Marketplace.

Si trabaja en un escenario conectado y si se ha registrado la instancia de la pila de Azure con Azure, puede descargar imagen de VM de Windows Server 2016 Hola de hello Azure Marketplace siguiendo los pasos de hello descritos en hello [descargar elementos del Marketplace de Azure tooAzure pila](azure-stack-download-azure-marketplace-item.md) tema.

Para obtener información acerca de cómo agregar diferentes elementos toohello marketplace, vea [hello Azure Marketplace de pila](azure-stack-marketplace.md).

## <a name="test-hello-offer"></a>Oferta de prueba Hola

Ahora que ha creado una oferta, puede probarla. Inicie sesión como un usuario y suscribirse toohello oferta y, a continuación, agregar una máquina virtual.

1. **Suscribirse tooan oferta**

   Ahora puede iniciar sesión en portal toohello como una oferta de tooan toosubscribe de usuario.

   a. En el equipo del Kit de implementación de pila de Azure de hello, inicie sesión demasiado`https://portal.local.azurestack.external` como un usuario y haga clic en **obtener una suscripción**.

   ![Obtener una suscripción](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   b. Hola **nombre para mostrar** campo, escriba un nombre para la suscripción, haga clic en **ofrecen**, haga clic en una de las ofertas de Hola Hola **elija una oferta** sección y, a continuación, haga clic en **Crear**.

   ![Creación de una oferta](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   c. suscripción de hello tooview que ha creado, haga clic en **más servicios**, haga clic en **suscripciones**, a continuación, haga clic en la nueva suscripción.  

   Después de suscribirse tooan oferta, actualice hello toosee portal los servicios que forman parte de la nueva suscripción de Hola.

2. **Aprovisionamiento de una máquina virtual**

   Ahora puede registrar en el portal de toohello como un usuario tooprovision una máquina virtual mediante suscripción Hola. 

   a. En el equipo del Kit de implementación de pila de Azure de hello, inicie sesión demasiado`https://portal.local.azurestack.external` como un usuario y, a continuación, haga clic en **New** > **proceso** > **centro de datos de Windows Server 2016 Eval**.  

   b. Hola **Fundamentos** sección, escriba un **nombre**, **nombre de usuario**, y **contraseña**. Para **Tipo de disco de máquina virtual**, elija **HDD**. Elija una **suscripción**. Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.  

   c. Hola **elegir un tamaño de** sección, haga clic en **A1 básica**y, a continuación, haga clic en **seleccione**.  

   d. Hola **configuración** sección, haga clic en **red Virtual**. Hola **red virtual de elegir** sección, haga clic en **crear nuevo**. Hola **crear red virtual** sección, acepte todos los valores predeterminados de Hola y haga clic en **Aceptar**. Hola **configuración** sección, haga clic en **Aceptar**.

   ![Creación de una red virtual](media/azure-stack-provision-vm/image04.png)

   e. Hola **resumen** sección, haga clic en **Aceptar** máquina virtual de toocreate Hola.  

   f. toosee la nueva máquina virtual, haga clic en **todos los recursos**, a continuación, busque la máquina virtual de Hola y haga clic en su nombre.

    ![Todos los recursos](media/azure-stack-provision-vm/image06.png)

En este tutorial aprendió:

> [!div class="checklist"]
> * Creación de una oferta
> * Añadir una imagen
> * Oferta de prueba Hola

> [!div class="nextstepaction"]
> [Asegúrese de web, móviles y los usuarios de API aplicaciones disponibles tooyour pila de Azure](azure-stack-tutorial-app-service.md)
