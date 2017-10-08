---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Tarea 3: habilitar LDAP seguro para hello dominio administrado mediante el portal de Azure clásico Hola
tooenable LDAP seguro, realizar Hola siguiendo los pasos de configuración:

1. Navegue toohello  **[portal de Azure clásico](https://manage.windowsazure.com)**.
2. Seleccione hello **Active Directory** nodo en el panel izquierdo de Hola.
3. Seleccione el directorio de hello Azure AD (también denominado tooas 'tenant'), que se han habilitado los servicios de dominio de AD de Azure.

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Haga clic en hello **configurar** ficha.

    ![Pestaña Configurar del directorio](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Desplácese hacia abajo de la sección de toohello **servicios de dominio de**. Debería ver una opción titulada **LDAP seguro (LDAPS)** tal y como se muestra en la siguiente captura de pantalla de hello:

    ![Sección de configuración de los Servicios de dominio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Haga clic en hello **configurar certificado...**  toobring botón seguridad hello **Configure un certificado para LDAP seguro** cuadro de diálogo.

    ![Configurar certificado para LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Haga clic en siguiente de icono de carpeta de hello **archivo PFX con certificado** archivo PFX de hello de toospecify, que contiene el certificado de hello desea toouse para toohello de acceso LDAP seguro administrado dominio. Especificar contraseña Hola especificado al exportar el archivo PFX de hello certificado toohello. A continuación, haga clic en hello realiza botón en la parte inferior de Hola.

    ![Especificar la contraseña y archivos PFX para LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Hola **los servicios de dominio** sección de hello **configurar** ficha debe obtener en gris y se encuentra en hello **pendientes...**  estado durante unos minutos. Durante este período, se comprueba el certificado LDAPS Hola para precisión y LDAP seguro está configurada para el dominio administrado.

    ![LDAP seguro: estado pendiente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Se tarda unos 10 minutos de too15 tooenable LDAP seguro para el dominio administrado. Si Hola proporcionado no coincide con el certificado LDAP seguro Hola necesario criterios, LDAP seguro no está habilitada para el directorio y verá un error. Por ejemplo, nombre de dominio de hello es incorrecto, el certificado de Hola ya ha expirado o va a expirar pronto.
   >
   >

9. Cuando LDAP seguro está habilitado correctamente para el dominio administrado, Hola **pendientes...**  mensaje debería desaparecer. Debería ver la huella digital de Hola de hello certificados que se muestran.

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Tarea 4: habilitar el acceso LDAP seguro a través de hello internet
**Tareas opcionales** : si no tiene previsto tooaccess Hola dominio administrado usa LDAPS más Hola a internet, omita esta tarea de configuración.

Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Debería ver una opción demasiado**Hola habilitar SECURE LDAP acceso a través de INTERNET** en hello **los servicios de dominio** sección de hello **configurar** página. Esta opción se establece demasiado**NO** de forma predeterminada porque internet access toohello administrada dominio a través de LDAP seguro está deshabilitado de forma predeterminada.

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Alternar **Hola habilitar SECURE LDAP acceso a través de INTERNET** demasiado**Sí**. Haga clic en hello **guardar** botón en el panel inferior Hola.
    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Hola **los servicios de dominio** sección de hello **configurar** ficha debe obtener en gris y se encuentra en hello **pendientes...**  estado durante unos minutos. Más tarde, está habilitado el acceso a internet tooyour dominio administrado a través de LDAP seguro.

    ![LDAP seguro: estado pendiente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Tarda aproximadamente 10 minutos tooenable acceso a internet a través de LDAP seguro para el dominio administrado.
   >
   >
4. Si tooyour de acceso LDAP seguro administra dominio a través Hola internet se habilitó correctamente, Hola **pendientes...**  mensaje debería desaparecer. Debería ver direcciones IP externas de Hola de direcciones que pueden ser utilizados tooaccess su directorio sobre LDAPS en campo hello **dirección de IP externas para acceso de LDAPS**.

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tarea 5: configurar DNS tooaccess Hola dominio administrado de hello internet
**Tareas opcionales** : si no tiene previsto tooaccess Hola dominio administrado usa LDAPS más Hola a internet, omita esta tarea de configuración.

Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 4](#task-4---enable-secure-ldap-access-over-the-internet).

Después de habilitar el acceso LDAP seguro a través de internet de hello para el dominio administrado, deberá tooupdate DNS para que los equipos cliente puedan encontrar este dominio administrado. Al final de saludo de la tarea 4, se muestra una dirección IP externa en hello **configurar** ficha **dirección de IP externas para acceso de LDAPS**.

Configurar el proveedor de DNS externo para que ese nombre DNS de Hola de hello administrados direcciones IP externas de dominio (por ejemplo, ' ldaps.contoso100.com') toothis puntos. En nuestro ejemplo, necesitamos hello toocreate siguiente entrada DNS:

    ldaps.contoso100.com  -> 52.165.38.113

¡Eso es todo: ya estás toohello tooconnect listo administrado Hola de dominio mediante LDAP seguro en internet.

> [!WARNING]
> Recuerde que los equipos cliente deben confiar emisor Hola de hello LDAPS certificado toobe pueda tooconnect correctamente toohello administrado dominio usa LDAPS. Si utilizas una entidad de certificación empresarial o una entidad de certificación de confianza pública, que no necesite toodo nada ya que estos emisores de certificados de confianza de los equipos cliente. Si está utilizando un certificado autofirmado, debe parte pública de hello tooinstall del certificado autofirmado de hello en el almacén de certificados de confianza de hello en el equipo cliente de Hola.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Bloquear LDAPS tener acceso a dominio administrado tooyour sobre Hola internet
> [!NOTE]
> **Tareas opcionales** : si no se ha habilitado LDAPS dominio administrado de acceso toohello en Hola internet, omita esta tarea de configuración.
>
>

Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 4](#task-4---enable-secure-ldap-access-over-the-internet).

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
