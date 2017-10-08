---
title: "Azure Active Directory Domain Services: Creación o selección de una red virtual | Microsoft Docs"
description: "Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Creación o selección de una red virtual para Azure Active Directory Domain Services
## <a name="before-you-begin"></a>Antes de empezar
Consulte demasiado[consideraciones de red para servicios de dominio de Active Directory de Azure](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Tarea 2: Creación de una red virtual de Azure
tarea de configuración siguiente Hello es toocreate una red virtual de Azure y una subred dentro de él. Puede habilitar Azure Active Directory Domain Services en esta subred dentro de la red virtual. Si tiene una red virtual existente que prefiere toouse, puede omitir este paso.

> [!NOTE]
> Asegúrese de que ese Hola red virtual de Azure cree o elija toouse con servicios de dominio de Active Directory de Azure pertenece tooan región de Azure es compatible con servicios de dominio de Active Directory de Azure. tooascertain Hola regiones de Azure en el que está disponible servicios de dominio de Active Directory de Azure, consulte [servicios de Azure por región](https://azure.microsoft.com/regions/#services/).
>
>Anote el nombre de Hola de hello tooensure de red virtual que seleccione red virtual derecha hello cuando se habilita servicios de dominio de Active Directory de Azure en un paso de configuración posteriores.


toocreate una red virtual de Azure en el que desea tooenable Azure Active Directory Domain Services, siga estas instrucciones de configuración:

1. Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el panel izquierdo de hello, seleccione **redes**.

    ![Nodo Redes](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Hola **redes virtuales** abre la ventana.
3. En el panel de tareas de hello en parte inferior de Hola de ventana hello, haga clic en **nuevo**.

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Haga clic en **Network Services** y seleccione **Virtual Network**.

    ![Red virtual: creación rápida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. Haga clic en una red virtual, toocreate **creación rápida**.

6. Especifique un **nombre** para su máquina de red y considere la posibilidad de acciones Hola siguientes:
    * Puede elegir tooconfigure **espacio de direcciones** o **recuento máximo de VM** para esta red.
    * Puede dejar hello **servidor DNS** establecer como **ninguno** por ahora. Puede actualizar la configuración de hello después de habilitar servicios de dominio de Active Directory de Azure.
7. Hola **ubicación** lista desplegable, seleccione una región de Azure admitida.  
    tooascertain Hola regiones de Azure en el que está disponible servicios de dominio de Active Directory de Azure, consulte [servicios de Azure por región](https://azure.microsoft.com/regions/#services/).
8. toocreate la red virtual, haga clic en **crear una red Virtual**.

    ![Creación de una red virtual para Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Después de crear una red virtual, seleccione Hola nombre de red virtual de hello y, a continuación, haga clic en hello **configurar** ficha.

    ![Creación de una subred](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. En **espacios de direcciones de red virtual**, haga clic en **Agregar subred**y, a continuación, especifique una subred con el nombre de hello **AaddsSubnet**.

    ![Creación de una subred para Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate Hola subred, haga clic en **guardar**.


## <a name="next-step"></a>Paso siguiente
[Tarea 3: Habilitación de Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)
