---
title: "Topologías admitidas de Azure AD Connect | Microsoft Docs"
description: "En este tema se detallan las topologías admitidas y no admitidas de Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologías de Azure AD Connect
Este artículo describen diversas topologías de Azure Active Directory (Azure AD) que usar la sincronización de Azure AD Connect como solución de integración clave de Hola y local. En este artículo se describen tanto las configuraciones admitidas como las no admitidas.

Aquí es leyenda Hola para las imágenes en el artículo hello:

| Descripción | Símbolo |
| --- | --- |
| Bosque local de Active Directory |![Bosque local de Active Directory](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| Instancia local de Active Directory con importación filtrada |![Active Directory con importación filtrada](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Servidor de Azure AD Connect Sync |![Servidor de Azure AD Connect Sync](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| "Modo de ensayo" del servidor de Azure AD Connect Sync |!["Modo de ensayo" del servidor de Azure AD Connect Sync](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync con Forefront Identity Manager (FIM) 2010 o Microsoft Identity Manager (MIM) 2016 |![GALSync con FIM 2010 o MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Servidor de Azure AD Connect Sync, información detallada |![Servidor de Azure AD Connect Sync, información detallada](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Escenario no admitido |![Escenario no admitido](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Un único bosque, un único inquilino de Azure AD
![Topología para un único bosque y un solo inquilino](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

topología más común de Hello es un único local del bosque, con uno o varios dominios y un anuncio de Azure único inquilino. Para la autenticación de Azure AD se utiliza la sincronización de contraseña. instalación rápida de Hola de Azure AD Connect admite sólo esta topología.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Bosque único, varios inquilinos de tooone Azure AD de servidores de sincronización
![Topología no admitida, filtrada para un único bosque](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Contar con varios servidores de sincronización de Azure AD Connect no se admite el inquilino conectado toohello mismo AD de Azure, con la excepción de un [servidor de ensayo](#staging-server). Tiene no compatibles incluso si estos servidores son toosynchronize configurado con un conjunto de objetos mutuamente excluyentes. Se debería considerar esta topología si no se puede llegar a todos los dominios en el bosque Hola desde un único servidor, o si desea toodistribute carga entre varios servidores.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Varios bosques, un único inquilino de Azure AD
![Topología para varios bosques y un solo inquilino](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Muchas organizaciones tienen entornos con varios bosques de Active Directory locales. Existen varias razones para tener más de un bosque de Active Directory local. Ejemplos típicos son diseños con el resultado de hello y bosques de recursos de la cuenta de una fusión o adquisición.

Cuando hay varios bosques, todos los bosques deben ser accesibles mediante un único servidor de Azure AD Connect Sync. No tiene dominio de toojoin Hola servidor tooa. Si es necesario tooreach todos los bosques, puede colocar el servidor de hello en una red perimetral (también conocida como DMZ, zona desmilitarizada y subred filtrada).

Asistente para la instalación de Hello Azure AD Connect ofrece varias opciones tooconsolidate quienes se representan en varios bosques. objetivo de Hello es que un usuario se representa una sola vez en Azure AD. Hay algunas topologías comunes que puede configurar en la ruta de acceso de instalación personalizada de hello en el Asistente para la instalación de Hola. En hello **identifica de forma única los usuarios** opción correspondiente Hola select que representa la topología de la página. consolidación de Hello está configurada solo para los usuarios. No se consolidan grupos duplicados con la configuración predeterminada de Hola.

Las topologías comunes se tratan en secciones de hello sobre [separar topologías](#multiple-forests-separate-topologies), [malla completa](#multiple-forests-full-mesh-with-optional-galsync), y [Hola topología cuenta recurso](#multiple-forests-account-resource-forest).

se da por supuesto la configuración predeterminada de Hello en Azure AD Connect sync:

* Cada usuario tiene una sola cuenta habilitada, y donde se encuentra esta cuenta de bosque de hello es usuario de Hola de tooauthenticate usado. Esta suposición es válida para la sincronización de contraseñas y para la federación. Los valores UserPrincipalName y sourceAnchor/immutableID proceden de este bosque.
* Cada usuario tiene un solo buzón de correo.
* bosque de Hola que hospeda el buzón de Hola para un usuario tiene Hola mejor calidad de los datos para los atributos visibles en hello lista Global de direcciones (GAL) de Exchange. Si no hay ningún buzón de usuario de hello, cualquier bosque puede ser toocontribute usa estos valores de atributo.
* Si tiene un buzón vinculado, también hay otra cuenta en otro bosque que se usa para el inicio de sesión.

Si su entorno no coincide con estas suposiciones, hello ocurrirá lo siguiente:

* Si tiene más de una cuenta activa o más de un buzón de correo, motor de sincronización de hello elige uno y omite Hola otro.
* Un buzón vinculado con ninguna otra cuenta activa no es tooAzure exportado AD. cuenta de usuario de Hello no se representa como un miembro de ningún grupo. Un buzón vinculado en DirSync siempre se representa como un buzón normal. Este cambio es intencionadamente un escenarios de varios bosques de soporte técnico de toobetter un comportamiento diferente.

Puede encontrar más detalles en [configuración predeterminada de descripción hello](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Varios bosques, varios inquilinos de tooone Azure AD de servidores de sincronización
![Topología no admitida para varios bosques y varios servidores de sincronización](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

No se admite tener tooa de servidor conectado de sincronización de Azure AD Connect más de un único a inquilino de Azure AD. excepción Hello es uso Hola de un [servidor de ensayo](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Varios bosques: topologías independientes
![Opción para representar los usuarios una sola vez en todos los directorios](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Representación de varios bosques y topologías independientes](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

En este entorno, todos los bosques locales se tratan como entidades independientes. Ningún usuario está presente en ningún otro bosque. Cada bosque tiene su propia organización de Exchange y no hay ningún GALSync entre bosques de Hola. Esta topología puede producirse una situación de hello después de una fusión o una adquisición o en una organización donde cada unidad de negocio funciona de forma independiente. Estos bosques están en Hola misma organización en Azure AD y aparecen con una GAL unificada. Hola delante de la imagen, cada objeto en cada bosque se representará una vez en el metaverso de Hola y se agregan en el inquilino de Azure AD de destino de Hola.

### <a name="multiple-forests-match-users"></a>Varios bosques: coincidencia de usuarios
Tooall comunes estos escenarios es que la distribución y grupos de seguridad pueden contener una combinación de usuarios, contactos y entidades de seguridad externa (FSP). FSP se utiliza en los miembros de toorepresent de servicios de dominio de Active Directory (AD DS) de otros bosques en un grupo de seguridad. FSP todos es objeto real toohello resuelto en Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Varios bosques: malla completa con GALSync opcional
![Opción para usar el atributo de correo de hello para la coincidencia cuando existen identidades de usuario en varios directorios](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Topología de malla completa para varios bosques](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Una topología de malla completa permite a los usuarios y toobe recursos ubicados en cualquier bosque. Normalmente, hay relación de confianza bidireccional entre los bosques de Hola.

Si Exchange está presente en más de un bosque, podría haber una solución GALSync local (opcional). Cada usuario se representaría como un contacto en todos los demás bosques. GALSync normalmente se implementa mediante FIM 2010 o MIM 2016. No se puede usar Azure AD Connect en GALSync local.

En este escenario, se combinan los objetos de identidad a través del atributo de correo de Hola. Un usuario que tiene un buzón de correo en un bosque se une con contactos de Hola Hola otros bosques.

### <a name="multiple-forests-account-resource-forest"></a>Varios bosques: bosque de cuenta-recurso
![Opción para usar atributos ObjectSID y msExchMasterAccountSID de hello para la coincidencia cuando existen identidades en varios directorios](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Topología de bosque de cuenta-recurso para varios bosques](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

En una topología de bosque de cuenta-recurso, tiene uno o más bosques de *cuentas* con cuentas de usuario activas. También tiene uno o más bosques de *recursos* con las cuentas deshabilitadas.

En este escenario uno (o más) bosques de recursos confían en todos los bosques de cuentas. bosque de recursos de Hello normalmente tiene un esquema de Active Directory extendido con Exchange y Lync. Todos los servicios de Exchange y Lync, así como otros servicios compartidos, se encuentran en este bosque. Los usuarios tienen una cuenta de usuario deshabilitada en este bosque, y se vincula el buzón de hello toohello bosque de cuentas.

## <a name="office-365-and-topology-considerations"></a>Consideraciones sobre la topología y Office 365
Algunas cargas de trabajo de Office 365 presentan ciertas restricciones en cuanto a las topologías compatibles:

| Carga de trabajo | Restricciones |
--------- | ---------
| Exchange Online | Si hay más de una organización de Exchange local (es decir, Exchange ha sido implementado toomore a un único bosque), debe utilizar Exchange 2013 SP1 o posterior. Consulte [Implementaciones híbridas con varios bosques de Active Directory](https://technet.microsoft.com/library/jj873754.aspx) para más información. |
| Skype Empresarial | Cuando se usa varios bosques locales, se admite solo topología de bosque de recursos de la cuenta de hello. Para más información, consulte los [requisitos de entorno de Skype para Business Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>servidor provisional
![Servidor de ensayo en una topología](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect admite la instalación de un segundo servidor en *modo de ensayo*. Un servidor en este modo lee los datos de todos los directorios conectados pero no escribir tooconnected directorios. Utiliza el ciclo de sincronización normal de hello y, por tanto, tiene una copia actualizada de los datos de identidad de Hola.

En un desastre donde se produce un error en servidor principal de hello, puede conmutar toohello servidor de almacenamiento provisional. Para ello, en el Asistente de Azure AD Connect de Hola. Este segundo servidor puede encontrarse en otro centro de datos porque ninguna infraestructura se comparte con el servidor principal de Hola. Debe copiar manualmente los cambios de configuración realizados en hello servidor principal toohello segundo servidor.

Puede usar un almacenamiento provisional tootest de servidor una nueva hello y configuración efecto personalizado que tiene en los datos. Puede obtener una vista previa de cambios de Hola y ajustar la configuración de Hola. Cuando esté satisfecho con la nueva configuración de hello, puede realizar Hola servidor activo de Hola de servidor de almacenamiento provisional y establecer el modo de toostaging de hello antiguo servidor activo.

También puede utilizar este servidor de active sync de método tooreplace Hola. Preparar el nuevo servidor de Hola y establezca su modo toostaging. Asegúrese de que está en buen estado, disable (hacerla activa), el modo de almacenamiento provisional y apagar el servidor activo actualmente Hola.

Es posible toohave más de un servidor de almacenamiento provisional cuando desee toohave varias copias de seguridad en distintos centros de datos.

## <a name="multiple-azure-ad-tenants"></a>Varios inquilinos de Azure AD
Recomendamos tener un único inquilino en Azure AD para una organización.
Antes de planear toouse varios inquilinos de Azure AD, consulte el artículo de hello [administración de unidades administrativas en Azure AD](../active-directory-administrative-units-management.md). Se ocupa de los escenarios comunes donde puede usar un solo inquilino.

![Topología para varios bosques y varios inquilinos](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Existe una relación 1:1 entre un servidor de Azure AD Connect Sync y un inquilino de Azure AD. Para cada inquilino de Azure AD, necesita una instalación de servidor de Azure AD Connect Sync. instancias de inquilino de Azure AD Hola están aislados por diseño. Es decir, los usuarios un inquilino no verán los usuarios de hello otro inquilino. Si desea esta separación, esta es una configuración admitida. En caso contrario, debe usar hello único modelo de inquilinos de Azure AD.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Cada objeto se incluye una sola vez en un inquilino de Azure AD
![Topología filtrada para un único bosque](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

En esta topología, un servidor de sincronización de Azure AD Connect es inquilino conectado tooeach Azure AD. servidores de sincronización de Azure AD Connect Hola deben configurarse para filtrar por lo que cada uno tiene un conjunto de objetos toooperate mutuamente excluyentes. Por ejemplo, puede definir el ámbito cada servidor tooa dominio o unidad organizativa.

Un dominio DNS solo se puede registrar en un único inquilino de Azure AD. Hola UPN de los usuarios de hello en la instancia de Active Directory local de hello también debe usar espacios de nombres independientes. Por ejemplo, en hello anterior imagen, tres sufijos UPN independientes se registran en la instancia de Active Directory local de hello: contoso.com y fabrikam.com, wingtiptoys.com. los usuarios de Hello en cada dominio de Active Directory local utilizar otro espacio de nombres.

No hay ningún GALSync entre instancias de inquilino de Azure AD Hola. Hola libreta de direcciones en Exchange Online y Skype de muestra de negocio solo los usuarios de Hola a mismo inquilino.

Esta topología tiene Hola restricciones en lo contrario los escenarios admiten:

* Solo uno de los inquilinos de hello Azure AD puede habilitar una implementación híbrida de Exchange con la instancia de Active Directory local de Hola.
* Los dispositivos de Windows 10 solo pueden asociarse con un inquilino de Azure AD.
* Hola única opción de sesión (SSO) para la autenticación de paso a través y de sincronización de contraseña puede utilizarse con un único inquilino de Azure AD.

requisito de Hola para un conjunto de objetos mutuamente excluyentes también aplica toowriteback. Algunas características de escritura diferida no se admiten con esta topología, porque estas asumen una sola configuración local. Estas características son:

* Escritura diferida de grupos con la configuración predeterminada.
* Escritura diferida de dispositivos.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Cada objeto se incluye varias veces en un inquilino de Azure AD
![Topología no admitida para un bosque único y varios inquilinos](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Topología no admitida para un bosque único y varios conectores](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

No se admiten las siguientes tareas:

* Sincronización Hola mismos inquilinos de Azure AD toomultiple de usuario.
* Realizar un cambio de configuración para que los usuarios de un directorio de Azure AD aparezcan como contactos en otro inquilino de Azure AD.
* Modificar a los inquilinos de Azure AD Connect sync tooconnect toomultiple Azure AD.

### <a name="galsync-by-using-writeback"></a>GALSync mediante escritura diferida
![Topología no admitida para varios bosques y varios directorios, con GALSync centrado en Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Topología no admitida para varios bosques y varios directorios, con GALSync centrado en una instancia de Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Los inquilinos de Azure AD están aislados por diseño. No se admiten las siguientes tareas:

* Cambiar configuración de Hola de datos de Azure AD Connect sync tooread desde otro inquilino de Azure AD.
* Exportar usuarios como instancia de Active Directory de contactos tooanother local mediante la sincronización de Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>GALSync con servidor de sincronización local
![GALSync en una topología para varios bosques y varios directorios](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

Puede usar FIM 2010 o MIM 2016 local toosync a los usuarios (a través de GALSync) entre dos organizaciones de Exchange. los usuarios de Hello en una organización aparecen como externa a los usuarios y contactos en Hola otra organización. Estas instancias de Active Directory locales se pueden sincronizar después con sus propios inquilinos de Azure AD.

## <a name="next-steps"></a>Pasos siguientes
toolearn tooinstall Azure AD Connect para estos escenarios, vea [instalación personalizada de Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
