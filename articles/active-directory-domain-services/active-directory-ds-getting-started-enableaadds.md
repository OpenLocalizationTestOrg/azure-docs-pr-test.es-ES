---
title: "Azure Active Directory Domain Services: habilitación de Azure Active Directory Domain Services | Microsoft Docs"
description: "Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Tarea 3: Habilitación de Azure Active Directory Domain Services
En esta tarea, habilitar Azure Active Directory Domain Services (Azure AD DS) para su directorio haciendo Hola pasos:

1. Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el panel izquierdo de hello, seleccione hello **Active Directory** botón.
3. Seleccione el inquilino de Azure Active Directory (Azure AD) de hello (directorio) que se desea tooenable Azure AD DS.

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. En hello **directorio de vista previa** página, haga clic en hello **configurar** ficha.

    ![Pestaña Configurar del directorio](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. En **los servicios de dominio**, cambiar hello **habilitar los servicios de dominio para este directorio** opción demasiado**Sí**.  
    Opciones de configuración de servicios de dominio de Active Directory de Azure adicionales aparecen en la página de Hola.

    ![Habilitación de los Servicios de dominio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Cuando se habilita Azure Servicios de dominio de Active Directory para el inquilino, Azure AD genera y almacena Hola Kerberos y NTLM hashes de credenciales que son necesarios para autenticar a los usuarios.
   >
   >
6. Especificar hello **nombre de dominio DNS de servicios de dominio**.

   * nombre de dominio predeterminado de Hello del directorio de hello (con un **. onmicrosoft.com** sufijo) está activada de forma predeterminada.

   * Hello lista contiene todos los dominios que se han configurado para su directorio Azure AD, las incluidas comprobado y no comprobados dominios que se configuran en hello **dominios** ficha.

   * También puede escribir un nombre de dominio personalizado. En este ejemplo, es el nombre de dominio personalizado de hello *contoso100.com*.

     > [!WARNING]
     > prefijo de Hola de su nombre de dominio especificado (por ejemplo, *contoso100* en hello *contoso100.com* nombre de dominio) debe contener 15 caracteres o menos. No se puede crear un dominio de Azure Active Directory Domain Services con un prefijo que contenga más de 15 caracteres.
     >
     >
7. Asegúrese de que ha elegido para hello administrado dominio todavía no existe en la red virtual de hello ese nombre de dominio DNS de Hola. En concreto, compruebe si toosee:

   * Ya tiene un dominio con hello mismo nombre de dominio DNS de red virtual de Hola.

   * Hello red virtual que ha seleccionado no tiene una conexión VPN con la red local y tiene un dominio con hello mismo nombre de dominio DNS de la red local.

   * Tiene un servicio en la nube con ese nombre de red virtual de Hola.
8. Seleccione una red virtual en el que desea toobe de servicios de dominio de Active Directory de Azure disponible. Seleccione la red virtual de Hola y subred dedicada que creó en hello **toothis de red virtual de servicios de dominio de conectar** lista desplegable. También tenga en cuenta los siguiente de hello:

   * Asegurarse de esa red virtual de Hola que ha especificado pertenece tooan región de Azure es compatible con servicios de dominio de Active Directory de Azure. tooascertain Hola regiones de Azure en servicios de dominio de Active Directory de Azure está disponible, consulte [servicios de Azure por región](https://azure.microsoft.com/regions/#services/).

   * Redes virtuales que pertenecen región tooa donde no se admite servicios de dominio de Active Directory de Azure no aparecen en la lista desplegable de Hola.

   * Utilice una subred dedicada dentro de la red virtual de Hola para servicios de dominio de Active Directory de Azure. Hacer *no* seleccione Hola subred de puerta de enlace. Consulte las [consideraciones sobre redes](active-directory-ds-networking.md).

   * De forma similar, las redes virtuales que se crearon mediante el Administrador de recursos de Azure no aparecen en la lista desplegable de Hola. Esto es porque las redes virtuales basadas en Resource Manager no son compatibles de momento con Azure Active Directory Domain Services.
9. Haga clic en tooenable Azure Active Directory Domain Services, en panel de tareas de hello en parte inferior de Hola de página de hello, **guardar**.
    * Mientras los servicios de dominio de Active Directory de Azure está habilitado para el directorio, página de hello muestra un estado de *pendiente*.

        ![Habilitación de la ventana Servicios de dominio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure Active Directory Domain Services proporciona una alta disponibilidad para el dominio administrado. Después de habilitar servicios de dominio de Active Directory de Azure, direcciones IP de hello en qué dominio de servicios están disponibles en la red virtual de hello son muestran uno a la vez. dirección IP de la segunda Hola se muestra en primer lugar, poco después de hello como pronto servicio Hola permite una alta disponibilidad para el dominio. Cuando se configura la alta disponibilidad y activo para su dominio, debería ver dos direcciones IP en hello **los servicios de dominio** sección de hello **configurar** ficha.
        >
        >
    * Después de aproximadamente 20 minutos de too30, primera dirección IP hello en qué dominio de servicios están disponibles en la red virtual en hello **dirección IP** campo hello **configurar** página.

        ![Ventana de Domain Services que muestra la primera dirección IP aprovisionada](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Cuando esté en funcionamiento para el dominio de alta disponibilidad, se muestran dos direcciones IP en la página de Hola. El dominio administrado está disponible en la red virtual seleccionada en estas dos direcciones IP.

10. Tenga en cuenta dos direcciones IP Hola para que pueda actualizar configuración de DNS de hello para la red virtual. Si lo hace, permite que las máquinas virtuales en dominio de toohello de tooconnect de red virtual de Hola para operaciones como la unión a un dominio.

    ![Ventana de Domain Services que muestra ambas direcciones IP aprovisionadas](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Según el tamaño de hello del inquilino de Azure AD (por ejemplo, el número de Hola de usuarios o grupos), el dominio de sincronización tooyour administrado tarda algún tiempo. Este proceso de sincronización se produce en segundo plano de Hola. Para inquilinos grandes con decenas de miles de objetos, puede tardar un día o dos para todos los usuarios, las pertenencias a grupos y toobe credenciales sincronizado.
>
>

## <a name="next-step"></a>Paso siguiente
[Tarea 4: actualizar la configuración de DNS de Hola de hello red virtual de Azure](active-directory-ds-getting-started-update-dns.md)
