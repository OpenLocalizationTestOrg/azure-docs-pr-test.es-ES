---
title: "Azure Active Directory Connect: Preguntas más frecuentes (P+F) | Microsoft Docs"
description: "Esta página contiene las preguntas más frecuentes sobre Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Preguntas más frecuentes acerca de Azure Active Directory Connect

## <a name="general-installation"></a>Instalación general
**P: ¿instalación funcionará si Hola administrador Global de Azure AD tiene 2FA habilitado?**  
Con las compilaciones de Hola de febrero de 2016, esto se admite.

**P: ¿existe una tooinstall de manera desatendida de Connect de Azure AD?**  
Es sólo compatible tooinstall Azure AD Connect con el Asistente para la instalación de Hola. No se admite la instalación silenciosa y desatendida.

**P: Tengo un bosque en el que no se puede contactar con un dominio. ¿Cómo se puede instalar Azure AD Connect?**  
Con las compilaciones de Hola de febrero de 2016, esto se admite.

**P: ¿Hola trabajo de agente de mantenimiento de AD DS en server core?**  
Sí. Después de instalar el agente de hello, puede completar el proceso de registro de hello mediante Hola siguiente cmdlet de PowerShell: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Red
**P: tengo un firewall, el dispositivo de red, o algo más que limita las conexiones de tiempo máximo de hello puede permanecer abierto en la red. ¿Cuál debería ser mi umbral de tiempo de espera del lado de cliente al usar Azure AD Connect?**  
Todo el software de red, dispositivos físicos o cualquier otra cosa que pueden permanecer abiertas las conexiones de tiempo máximo de hello debe usar un umbral de al menos 5 minutos (300 segundos) para la conectividad entre los límites Hola servidor hello Azure AD Connect cliente está instalado y Azure Active Directory. Esto también aplica la herramienta de sincronización de Microsoft Identity tooall que anteriormente se publicó.

**P: ¿Se admiten los dominios de una sola etiqueta (SLD)?**  
 No, Azure AD Connect no admite bosques/dominios locales con dominios de una sola etiqueta.

**P: ¿Se admiten los nombres de NetBios con puntos?**  
No, Azure AD Connect no admite local bosques o dominios donde el nombre de NetBios de hello contiene un punto "." en nombre de Hola.

## <a name="federation"></a>Federación
**P: ¿qué debo hacer si se recibe un correo electrónico que me pide toorenew mi certificado de Office 365**  
Utilizar la Guía de hello descrito en hello [renovar certificados](active-directory-aadconnect-o365-certs.md) tema acerca de cómo toorenew Hola certificado.

**P.: Tengo establecido Actualizar automáticamente el usuario de confianza para el usuario de confianza de O365. ¿Tengo tootake ninguna acción cuando se sustituye el token de certificado de firma automáticamente?**  
Utilizar la Guía de Hola que se describe en el artículo de hello [renovar certificados](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Environment
**P: ¿es sólo admitido toorename Hola server después de que se ha instalado Azure AD Connect?**  
No. Cambiar el nombre de servidor hello será causa Hola sincronización motor toonot base de datos SQL puede tooconnect toohello y servicio hello no será capaz de toostart.

## <a name="identity-data"></a>Datos de identidad
**P: no coincide con el atributo UPN (userPrincipalName) hello en Azure AD Hola UPN local: ¿por qué?**  
 Consulte estos artículos:

* [Nombres de usuario no coinciden en Office 365, Azure ni Intune Hola UPN local o Id. de inicio de sesión alternativo](https://support.microsoft.com/en-us/kb/2523192)
* [Los cambios no se sincronizan mediante la herramienta de sincronización de Azure Active Directory Hola después de cambiar Hola UPN de un toouse de cuenta de usuario un dominio federado diferente](https://support.microsoft.com/en-us/kb/2669550)

También puede configurar Azure AD tooallow Hola sincronización motor tooupdate Hola userPrincipalName tal y como se describe en [características del servicio de sincronización de Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**P: ¿son compatible toosoft coincidencia locales objetos de grupo o contacto de AD con objetos de grupo o contacto de Azure AD existente?**  
No, actualmente no se admite.

**P: ¿es toomanually de TI admitida establece el atributo de ImmutableId en Azure AD grupo o contacto existente objetos toohard coincidir local tooon objetos de grupo o contacto de AD?**  
No, actualmente no se admite.



## <a name="custom-configuration"></a>Configuración personalizada
**P: ¿dónde son Hola cmdlets de PowerShell para Azure AD Connect documentado?**  
Con excepción de Hola de cmdlets de hello documentados en este sitio, no se admiten otros cmdlets de PowerShell que se encuentra en Azure AD Connect para uso del cliente.

**P: ¿puedo usar la "Importación / servidor de exportación de servidor" se encuentra en *Synchronization Service Manager* toomove configuración entre servidores?**  
No. Esta opción no recuperará todas las opciones de configuración y no debe usarse. En su lugar debe usar configuración básica de hello Asistente toocreate hello en el segundo servidor de Hola y usar reglas de sincronización Hola editor toogenerate PowerShell scripts toomove cualquier regla personalizada entre servidores. Consulte [Migración oscilante](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**P: ¿pueden las contraseñas almacenarse en caché para la página de Hola de inicio de sesión Azure y esto se puede evitar que porque contiene un elemento input de contraseña con Autocompletar hello = "false" atributo?**</br>
Actualmente no admitimos modificación Hola de atributos HTML del campo de entrada de contraseña hello, incluyendo Hola Autocompletar etiqueta. Actualmente estamos trabajando en una característica que le permitirá para Javascript personalizado que le permitirá tooadd cualquier campo de contraseña de toohello de atributo. Esta solución debería estar disponible a finales de 2017.

**P: ¿en hello Azure página de inicio de sesión, se muestran los nombres de usuario para los usuarios que previamente han iniciado sesión correctamente.  ¿Este comportamiento se puede desactivar?**</br>
Actualmente no admitimos modificación Hola de atributos HTML de la página de inicio de sesión de Hola. Actualmente estamos trabajando en una característica que le permitirá para Javascript personalizado que le permitirá tooadd cualquier campo de contraseña de toohello de atributo. Esta solución debería estar disponible a finales de 2017.

**P: ¿existe una manera tooprevent sesiones simultáneas?**</br>
No.



## <a name="troubleshooting"></a>Solución de problemas
**P: ¿Cómo puedo obtener ayuda con Azure AD Connect?**

[Buscar Hola Microsoft Knowledge Base (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Busque en Microsoft Knowledge Base (KB) de Hola para problemas de soluciones técnicas toocommon break-fix en línea sobre la compatibilidad con Azure AD Connect.

[Foros de Microsoft Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Puede buscar y examinar para technical preguntas y respuestas de la Comunidad de Hola o Formula su pregunta haciendo clic en [aquí](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Asistencia al cliente de Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Use esta compatibilidad de tooget de vínculo a través de hello portal de Azure.

