---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)


## <a name="before-you-begin"></a>Antes de empezar
Consulte demasiado[consideraciones de red para servicios de dominio de Active Directory de Azure](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Tarea 2: Configuración de red
tarea de configuración siguiente Hello es toocreate una red virtual de Azure y una subred dedicada dentro de él. Puede habilitar Azure Active Directory Domain Services en esta subred dentro de la red virtual. También puede elegir una red virtual existente y crear una subred de hello dedicado dentro de él.

1. Haga clic en **red Virtual** tooselect una red virtual.
2. En hello **red virtual de elegir** hoja, verá todas las redes virtuales existentes. Vea solo Hola redes virtuales que pertenecen a grupo de recursos de toohello y ubicación de Azure que seleccionó en hello **Fundamentos** página del asistente.

3. Elija la red virtual de hello en el que deben habilitarse servicios de dominio de AD de Azure. Haga clic en **crear nuevo**, si lo prefiere toocreate una nueva red virtual. Se recomienda usar una subred dedicada para Azure AD Domain Services. Si elige una red virtual existente, [crear una subred dedicada con la extensión de redes virtuales de hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) y, a continuación, seleccione esa subred. 

    ![Seleccionar una red virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Haga clic en **subred** toopick Hola subred dedicada en esta red virtual, en qué tooenable su nuevo administrado dominio. Hola **crear subred** hoja, especifique un nombre para la subred de Hola y haga clic en **Aceptar** cuando haya terminado. Por ejemplo, puede crear una subred con el nombre de hello 'DomainServices', lo que facilita para otro administradores toounderstand lo que se implementa dentro de la subred de Hola.

    ![Seleccione la subred de red virtual de Hola](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Directrices para seleccionar una subred**
  > 1. Use una subred dedicada para Azure AD Domain Services. No se implementa ninguna otra subred de toothis de máquinas virtuales. Esta configuración permite a tooconfigure grupos de seguridad de red (NSG) para las máquinas virtuales o las cargas de trabajo sin interrumpir el dominio administrado. Para obtener detalles, vea [Consideraciones de red de Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. No seleccione subred de puerta de enlace de Hola para implementar los servicios de dominio de Active Directory de Azure, porque no es una configuración admitida.
  3. Asegúrese de que ha seleccionado la subred hello tiene suficiente espacio de direcciones disponible - direcciones IP disponibles de al menos 3 a 5.
  >

5. Cuando haya terminado, haga clic en **Aceptar** toomove en toohello **grupo de administradores** página del Asistente para saludo.


## <a name="next-step"></a>Paso siguiente
[Tarea 3: Configuración del grupo administrativo y habilitación de Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
