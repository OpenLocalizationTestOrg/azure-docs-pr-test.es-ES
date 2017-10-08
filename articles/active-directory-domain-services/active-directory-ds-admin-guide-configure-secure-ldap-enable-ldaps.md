---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services

## <a name="before-you-begin"></a>Antes de empezar
Asegúrese de que ha completado [tarea 2: exportar Hola segura LDAP certificado tooa. Archivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Elegir entre toouse hello Azure experiencia del portal de vista previa o hello Azure toocomplete portal clásico esta tarea.
> [!div class="op_single_selector"]
> * **Portal de Azure (vista previa)**: [Enable secure LDAP mediante Hola portal de Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Portal de Azure clásico**: [Enable secure LDAP mediante el portal de Azure clásico Hola](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Tarea 3: habilitar LDAP seguro de dominio administrados de hello mediante Hola portal de Azure (vista previa)
tooenable LDAP seguro, realizar Hola siguiendo los pasos de configuración:

1. Navegue toohello  **[portal de Azure](https://portal.azure.com)**.

2. Busque "servicios de dominio' en hello **buscar recursos** cuadro de búsqueda. Seleccione **servicios de dominio de AD de Azure** Hola resultados de búsqueda. Hola **servicios de dominio de AD de Azure** hoja muestra el dominio administrado.

    ![Búsqueda del dominio administrado que se va aprovisionar](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Haga clic en Hola Hola administrado toosee de dominio (por ejemplo, ' contoso100.com') para obtener más detalles sobre el dominio de Hola.

    ![Domain Services: estado de aprovisionamiento](./media/getting-started/domain-services-provisioning-state.png)

3. Haga clic en **LDAP seguro** en el panel de navegación de Hola.

    ![Hoja Servicios de dominio: LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. De forma predeterminada, LDAP acceso tooyour administrado dominio seguro está deshabilitado. Alternar **LDAP seguro** demasiado**habilitar**.

    ![Habilitación de LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. De forma predeterminada, tooyour de acceso LDAP seguro administra dominio a través de hello que Internet está deshabilitada. Alternar **Hola a permitir acceso LDAP seguro a través de internet** demasiado**habilitar**, si lo desea. 

6. Haga clic en siguiente de icono de carpeta de hello **. Archivo PFX con certificado LDAP seguro**. Especifique archivo PFX de hello ruta de acceso toohello con certificado de Hola para LDAP acceso toohello administrado dominio seguro.

7. Especificar hello **toodecrypt de contraseña. Archivo PFX**. Proporcionar Hola contraseña que se usa al exportar el archivo PFX de hello certificado toohello.

8. Cuando haya terminado, haga clic en hello **guardar** botón.

9. Verá una notificación que le informa de que LDAP seguro se configura de dominio administrados Hola. Hasta que se complete esta operación, no se puede modificar otras configuraciones de dominio de Hola.

    ![Configuración de LDAP seguro para el dominio administrado Hola](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Se tarda unos 10 minutos de too15 tooenable LDAP seguro para el dominio administrado. Si Hola proporcionado no coincide con el certificado LDAP seguro Hola necesario criterios, LDAP seguro no está habilitada para el directorio y verá un error. Por ejemplo, nombre de dominio de hello es incorrecto, el certificado de Hola ya ha expirado o va a expirar pronto. En este caso, vuelva a intentarlo con un certificado válido.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tarea 4: configurar DNS tooaccess Hola dominio administrado de hello internet
> [!NOTE]
> **Tareas opcionales** : si no tiene previsto tooaccess Hola dominio administrado usa LDAPS más Hola a internet, omita esta tarea de configuración.
>
>

Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Después de habilitar el acceso LDAP seguro a través de internet de hello para el dominio administrado, deberá tooupdate DNS para que los equipos cliente puedan encontrar este dominio administrado. Al final de Hola de tarea 3, se muestra una dirección IP externa en hello **propiedades** hoja en **dirección de IP externas para acceso de LDAPS**.

Configurar el proveedor de DNS externo para que ese nombre DNS de Hola de hello administrados direcciones IP externas de dominio (por ejemplo, ' ldaps.contoso100.com') toothis puntos. En nuestro ejemplo, necesitamos hello toocreate siguiente entrada DNS:

    ldaps.contoso100.com  -> 52.165.38.113

¡Eso es todo: ya estás toohello tooconnect listo administrado Hola de dominio mediante LDAP seguro en internet.

> [!WARNING]
> Recuerde que los equipos cliente deben confiar emisor Hola de hello LDAPS certificado toobe pueda tooconnect correctamente toohello administrado dominio usa LDAPS. Si utilizas una entidad de certificación de confianza pública, que no necesite toodo nada ya que estos emisores de certificados de confianza de los equipos cliente. Si está utilizando un certificado autofirmado, instale parte pública de Hola de certificado autofirmado de hello en el almacén de certificados de confianza de hello en el equipo cliente de Hola.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Tarea 5: bloquear LDAPS acceso tooyour administrado Hola de dominio a través de internet
> [!NOTE]
> **Tareas opcionales** : si no se ha habilitado LDAPS dominio administrado de acceso toohello en Hola internet, omita esta tarea de configuración.
>
>

Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Exposición de su dominio administrado para el acceso LDAPS sobre Hola internet representa una amenaza para la seguridad. Hello dominio administrado sea accesible desde Hola internet en el puerto de hello usado para LDAP seguro (es decir, el puerto 636). Por lo tanto, puede elegir toorestrict acceso toohello administrado dominio toospecific conocida direcciones IP. Para mejorar la seguridad, cree un grupo de seguridad de red (NSG) y asociarla a la subred de Hola donde ha habilitado los servicios de dominio de AD de Azure.

Hello siguiente tabla muestra un ejemplo de NSG puede configurar, toolock hacia abajo el acceso LDAP seguro a través de hello internet. Hola NSG contiene un conjunto de reglas que permitan el acceso de entrada LDAPS a través del puerto TCP 636 solo de un conjunto especificado de direcciones IP. Hello 'DenyAll' reglas predeterminadas aplican tooall otro tráfico entrante de hello internet. regla de acceso LDAPS NSG tooallow sobre Hola Hola internet desde direcciones IP especificadas tiene una prioridad más alta que Hola regla DenyAll NSG.

![Acceso de ejemplo NSG toosecure LDAPS sobre Hola internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Más información** - [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services](active-directory-ds-admin-guide-administer-group-policy.md)
* [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md)
* [Creación de un grupo de seguridad de red](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
