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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Habilitación de Azure Active Directory Domain Services (versión preliminar)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Tarea 4: actualizar la configuración de DNS para hello red virtual de Azure
Hola anterior tareas de configuración, ha habilitado correctamente Azure Servicios de dominio de Active Directory para su directorio. Hola siguiente tarea es tooensure que los equipos de red virtual de hello pueden conectarse y usar estos servicios. En este artículo, se actualiza la configuración de servidor DNS de Hola para sus red virtual toopoint toohello dos direcciones IP en servicios de dominio de Active Directory de Azure está disponible en la red virtual de Hola.

configuración de servidor de tooupdate Hola DNS para la red virtual de hello en el que ha habilitado Azure Active Directory Domain Services, completa Hola pasos:

1. Hola **Introducción** ficha enumera un conjunto de **requiere pasos de configuración** toobe realiza después de que el dominio administrado está aprovisionado por completo. es el primer paso de configuración Hello **configuración del servidor DNS de la actualización de la red virtual**.

    ![Domain Services: pestaña Información general después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned-overview.png)

2. Cuando el dominio está completamente aprovisionado, se muestran dos direcciones IP en este icono. Cada una de estas direcciones IP representa un controlador de dominio en el dominio administrado.

3. toocopy Hola primera dirección IP tooclipboard de direcciones, haga clic en botón de copia hello tooit siguiente. A continuación, haga clic en hello **servidores DNS configurar** botón.

4. Pegue la dirección IP de la primera hello en hello **servidor DNS agregar** cuadro de texto en hello **servidores DNS** hoja. Desplazarse horizontalmente toohello dejado la segunda dirección IP de toocopy hello y pegarlos en hello **servidor DNS agregar** cuadro de texto.

    ![Domain Services: actualización de DNS](./media/getting-started/domain-services-update-dns.png)

5. Haga clic en **guardar** cuando haya terminado los servidores DNS de tooupdate hello para la red virtual de Hola.

> [!NOTE]
> Máquinas virtuales de red de hello solo obtiene la configuración de DNS nueva de hello después del reinicio. Si necesita configuración DNS de tooget Hola actualiza inmediatamente, desencadenar un reinicio del portal de hello, PowerShell u Hola CLI.
>
>

## <a name="next-step"></a>Paso siguiente
[Tarea 5: habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory](active-directory-ds-getting-started-password-sync.md)
