---
title: "Azure Active Directory Domain Services: Actualizar configuración de DNS para hello red virtual de Azure | Documentos de Microsoft"
description: "Introducción a los Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Actualizar la configuración de DNS para hello red virtual de Azure
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Tarea 4: Actualizar valores de DNS para hello red virtual de Azure
Hola anterior tareas de configuración, ha habilitado correctamente Azure Servicios de dominio de Active Directory para su directorio. Hola siguiente tarea es tooensure que los equipos de red virtual de hello pueden conectarse y usar estos servicios. En este artículo, se actualiza la configuración de servidor DNS de Hola para sus red virtual toopoint toohello dos direcciones IP en servicios de dominio de Active Directory de Azure está disponible en la red virtual de Hola.

> [!NOTE]
> Después de habilitar Azure Servicios de dominio de Active Directory para el directorio de hello, tenga en cuenta las direcciones IP Hola para Azure Active Directory Domain Services que se muestran en hello **configurar** pestaña del directorio.
>
>

configuración de servidor de tooupdate Hola DNS para la red virtual de hello en el que ha habilitado Azure Active Directory Domain Services, completa Hola pasos:

1. Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el panel izquierdo de hello, seleccione **redes**.  
    Hola **redes** abre la ventana.

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. En hello **redes virtuales** ficha, en el que ha habilitado Servicios de dominio de Active Directory de Azure tooview sus propiedades de red virtual seleccione Hola.
4. Haga clic en hello **configurar** ficha.

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. Hola **servidores DNS** sección, escriba dos direcciones IP de Hola que se mostraron en hello **los servicios de dominio** sección en hello **configurar** pestaña del directorio.
6. Haga clic en configuración del servidor DNS toosave Hola para esta red virtual, en panel de tareas de hello en parte inferior de Hola de ventana hello, **guardar**.

   ![Actualizar la configuración de servidor DNS de hello para la red virtual de Hola](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Máquinas virtuales de red de hello solo obtiene la configuración de DNS nueva de hello después del reinicio. Si necesita configuración DNS de tooget Hola actualiza inmediatamente, desencadenar un reinicio del portal de hello, PowerShell u Hola CLI.
>
>

## <a name="next-steps"></a>Pasos siguientes
Tarea 5: [habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory](active-directory-ds-getting-started-password-sync.md)
