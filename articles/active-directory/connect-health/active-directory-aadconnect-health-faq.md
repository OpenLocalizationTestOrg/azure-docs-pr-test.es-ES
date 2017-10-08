---
title: "aaaAzure Active Directory conectarse mantenimiento Preguntas más frecuentes: Azure | Documentos de Microsoft"
description: "Las preguntas más frecuentes son preguntas y respuestas sobre Azure AD Connect Health. Estas preguntas más frecuentes abordan los problemas sobre el uso de servicio de hello, incluido el modelo, las capacidades, limitaciones y soporte técnico de facturación de Hola."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Preguntas más frecuentes sobre Azure AD Connect Health
Este artículo incluye toofrequently respuestas preguntas frecuentes (P+f) sobre el estado de conexión de Azure Active Directory (Azure AD). Estas preguntas más frecuentes incluyen preguntas acerca de cómo toouse Hola servicio, que incluye el modelo, las capacidades, limitaciones y soporte técnico de facturación de Hola.

## <a name="general-questions"></a>Preguntas generales
**P: Administro varios directorios de Azure AD. ¿Cómo se puede cambiar el toohello uno con Azure Active Directory Premium?**

tooswitch entre diferentes Azure AD a los inquilinos, seleccione Hola actualmente inició sesión **nombre de usuario** en Hola esquina superior derecha y, a continuación, elija la cuenta adecuada de Hola. Si la cuenta de hello no aparece aquí, seleccione **cerrar sesión**, y, a continuación, usar credenciales de administrador global de hello del directorio de hello con Azure Active Directory Premium habilitan toosign en.

**P: ¿Qué versión de los roles de identidad es compatible con Azure AD Connect Health?**

Hello tabla siguiente enumera las funciones hello y admite versiones de sistema operativo.

|Rol| Sistema operativo/versión|
|--|--|
|Active Directory Federation Services (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Versión 1.0.9125 o posterior.|
|Active Directory Domain Services (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Tenga en cuenta que pueden diferir características Hola proporcionadas por el servicio de hello basada en función de Hola y sistema operativo de Hola. En otras palabras, todas las características de hello no estén disponibles para todas las versiones de sistema operativo. Ver una descripción de la característica de Hola para obtener más información.

**P: ¿cuántas licencias es necesario toomonitor mi infraestructura?**

* Hello primer agente de mantenimiento de conexión requiere al menos una licencia de Azure AD Premium.
* Cada agente adicional registrado requiere otras 25 licencias Premium de Azure AD.
* Número de agentes es equivalente toohello el número total de agentes que están registrados en todos los roles supervisados (AD FS, Azure AD Connect o AD DS).

Información de licencia se encuentra también en hello [página de precios de Azure AD](https://aka.ms/aadpricing).

Ejemplo:

| Agentes registrados | Licencias necesarias | Ejemplo de configuración de supervisión |
| ------ | --------------- | --- |
| 1 | 1 | 1 servidor de AAD Connect |
| 2 | 26| 1 servidor de Azure AD Connect y 1 controlador de dominio |
| 3 | 51 | 1 servidor de Active Directory Federation Services (AD FS), 1 proxy de AD FS y 1 controlador de dominio |
| 4 | 76 | 1 servidor de AD FS, 1 proxy de AD FS y 2 controladores de dominio |
| 5 | 101 | 1 servidor de Azure AD Connect, 1 servidor de AD FS, 1 proxy de AD FS y 2 controladores de dominio |


## <a name="installation-questions"></a>Preguntas sobre instalación

**P: ¿cuál es el impacto de saludo de la instalación de agente de Azure AD Connect Health hello en servidores individuales?**

impacto de saludo de la instalación de servidores de proxy de aplicación web de hello agente Microsoft Azure AD Connect Health, AD FS, los servidores de Azure AD Connect (sync), controladores de dominio es mínima con respecto toohello CPU, consumo de memoria, ancho de banda de red y almacenamiento.

Hola siguiendo los números es una aproximación:

* Consumo de CPU: aumento de ~1-5 %.
* Consumo de memoria: % too10 Hola total de memoria del sistema.

> [!NOTE]
> Si el agente de hello no puede comunicarse con Azure, agente Hola almacena los datos de hello localmente para un límite máximo definido. agente de Hello sobrescribe Hola "en caché" datos de forma "atiende menos recientemente".
>
>

* Almacenamiento en búfer local para Agentes de Azure AD Connect Health: ~20 MB.
* Para los servidores de AD FS, se recomienda aprovisionar a un espacio en disco de 1024 MB (1 GB) para el canal de auditoría de hello AD FS para agentes de Azure AD Connect Health tooprocess todos los datos de auditoría de hello antes de que se sobrescribe.

**P: ¿tendré tooreboot Mis servidores durante la instalación de Hola de agentes de mantenimiento de hello Azure AD Connect?**

No. instalación de Hola de agentes de hello no requerirá servidor hello tooreboot. Sin embargo, la instalación de algunos pasos de requisitos previos puede requerir un reinicio del servidor hello.

Por ejemplo, en Windows Server 2008 R2, la instalación de .Net 4.5 Framework requiere un reinicio del servidor.

**P: ¿Funciona Azure AD Connect Health mediante un proxy HTTP de paso?**

Sí. Para las operaciones en curso, puede configurar toouse de agente de mantenimiento de hello un solicitudes HTTP de la salida de tooforward del proxy HTTP.
Lea más sobre cómo [configurar el proxy HTTP para los agentes de mantenimiento](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Si necesita tooconfigure un servidor proxy durante el registro del agente, tendrá que toomodify la configuración de Proxy de Internet Explorer con antelación.

1. Abra Internet Explorer > **Configuración** > **Opciones de Internet** > **Conexiones** > **Configuración de LAN**.
2. Seleccione **Usar un servidor proxy para la LAN**.
3. Seleccione **Opciones avanzadas** si tiene distintos puertos de proxy para HTTP y HTTPS/Secure.

**P: ¿autenticación básica de soporte técnico de Azure AD Connect Health al conectarse a servidores proxy tooHTTP?**

No. Un mecanismo toospecify un nombre de usuario arbitrarios y una contraseña para la autenticación básica no se admite actualmente.

**P: ¿qué puertos del firewall hacer necesito tooopen para toowork de conectar el agente de mantenimiento de hello Azure AD?**

Vea hello [sección Requisitos](active-directory-aadconnect-health-agent-install.md#requirements) lista de Hola de puertos del firewall y otros requisitos de conectividad.

**P: ¿por qué veo dos servidores con hello igual nombre en hello Azure AD Connect Health portal?**

Cuando se quita un agente de un servidor, servidor hello no se quita automáticamente del portal de Azure AD Connect Health Hola. Si elimina a un agente desde un servidor o quitar el propio servidor hello manualmente, debe entrada del servidor hello toomanually delete desde el portal de hello Azure AD Connect Health.

Puede restablecer imagen inicial de un servidor o crear un nuevo servidor con hello detalles del mismo (por ejemplo, nombre de equipo). Si no quitó Hola ya registrados servidor de portal de hello Azure AD Connect Health e instalar agente de hello en el nuevo servidor de hello, puede ver dos entradas con hello mismo nombre.

En este caso, elimine manualmente la entrada de Hola que pertenece el servidor antiguo toohello. datos Hola para este servidor deben estar obsoletas.

## <a name="health-agent-registration-and-data-freshness"></a>Registro del agente de mantenimiento y actualización de datos

**P: ¿Cuáles son los motivos comunes para errores de registro del agente de mantenimiento de Hola y cómo solucionar problemas?**

Hello agente de mantenimiento puede producir un error tooregister debido toohello siguiente posibles razones:

* agente de Hello no puede comunicarse con extremos de hello necesario porque un firewall está bloqueando el tráfico. Esto es especialmente frecuente en servidores proxy de aplicación web. Asegúrese de que haya permitido puertos y los puntos de conexión de comunicaciones de salida toohello necesario. Vea hello [sección Requisitos](active-directory-aadconnect-health-agent-install.md#requirements) para obtener más información.
* Comunicación de salida es tooan sometidos inspección de SSL mediante la capa de red Hola. Esto hace que certificado de Hola Hola emplea toobe reemplazado por entidad/servidor de inspección de hello, y producirá un error en el registro del agente Hola pasos toocomplete Hola.
* Hola usuario no tiene acceso tooperform Hola registro del agente de Hola. Los administradores globales tienen acceso de forma predeterminada. Puede usar [Control de acceso basado en roles](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate tooother de acceso los usuarios.

**P: ¿Estoy obteniendo una alerta que "datos de servicio de mantenimiento no están una toodate." ¿Cómo se puede solucionar el problema de hello?**

Azure AD Connect Health genera alerta Hola si no recibe todos los puntos de datos de Hola de servidor Hola Hola últimas dos horas. Los motivos de esta alerta pueden ser varios.

* agente de Hello no puede comunicarse con extremos de hello necesario porque un firewall está bloqueando el tráfico. Esto es especialmente frecuente en servidores proxy de aplicación web. Asegúrese de que haya permitido la comunicación saliente toohello necesario dos puntos finales y los puertos. Vea hello [sección Requisitos](active-directory-aadconnect-health-agent-install.md#requirements) para obtener más información.
* Comunicación de salida es tooan sometidos inspección de SSL mediante la capa de red Hola. Esto hace que certificado de Hola Hola emplea toobe reemplazado por entidad/servidor de inspección de hello y, proceso de hello produce un error en el servicio de mantenimiento de Azure AD Connect de tooupload datos toohello.
* Puede usar el comando de conectividad de hello integrado en el agente de Hola. [Más información](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* agentes de Hello también admiten conectividad saliente a través de un HTTP Proxy no autenticadas. [Más información](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Preguntas sobre operaciones
**P: ¿necesito tooenable auditoría en servidores de proxy de aplicación de hello web?**

No, la auditoría no es necesario toobe habilitado en servidores de proxy de aplicación web de Hola.

**P: ¿Cómo se resuelven las alertas de Azure AD Connect Health?**

Las alertas de Azure AD Connect Health se resuelven en una condición satisfactoria. Agentes de Azure AD Connect Health detectar y notificar Hola exitoso condiciones toohello servicio periódicamente. Para algunas alertas, supresión de hello está basado en el tiempo. En otras palabras, si hello misma condición de error no se observa en 72 horas desde la generación de alertas, alertas de Hola se resuelven automáticamente.

**P: ¿Estoy obteniendo una alerta que "solicitud de autenticación de prueba (transacción sintética) no pudo tooobtain un símbolo (token)." ¿Cómo se puede solucionar el problema de hello?**

Azure AD Connect Health para AD FS genera esta alerta cuando Hola agente de mantenimiento instalado en un servidor de AD FS no puede tooobtain un token como parte de una transacción sintética iniciada por el agente de mantenimiento de Hola. agente de mantenimiento de Hello usa el contexto del sistema local de Hola y trata tooget un token para un usuario de confianza propio. Se trata de un tooensure de prueba de detección de todos los que AD FS se encuentra en un estado de emisión de tokens.

Con mayor frecuencia esta prueba produce un error porque Hola agente de mantenimiento es el nombre de granja de servidores de hello AD FS de tooresolve no se puede. Esto puede ocurrir si los servidores de hello AD FS están detrás de equilibradores de carga de red y solicitud Hola obtiene iniciada desde un nodo que está detrás de equilibrador de carga de hello (como tooa opuestos de cliente normal que se encuentra delante de equilibrador de carga de hello). Esto se puede solucionar mediante la actualización de archivo de hosts"hello" ubicado en tooinclude de dirección IP "C:\Windows\System32\drivers\etc" hello del servidor de AD FS de Hola o una dirección IP de bucle invertido (127.0.0.1) para el nombre de la granja de AD FS hello (por ejemplo, sts.contoso.com). Agregar archivos de host de Hola cortocircuito llamada de red de hello, por lo que el token de hello agente de mantenimiento tooget Hola.

**P: tengo un correo electrónico que indica que mis equipos no se han modificado para ataques de ransomeware reciente Hola. ¿Por qué he recibido este correo electrónico?**

Servicio de Azure AD Connect Health analiza Hola todas las máquinas supervisa tooensure revisiones de hello necesario se instalaron. correo electrónico de Hello envió los administradores de inquilinos de toohello si al menos una máquina no tenía revisiones críticas Hola. Hola siguientes lógica se ha usado toomake esta determinación.
1. Buscar todas las revisiones de hello instaladas en el equipo de Hola.
2. Compruebe si al menos uno de hello las revisiones de hello definido lista está presente.
3. En caso afirmativo, la máquina de hello está protegida. Si no es así, máquina hello es un riesgo de ataques de Hola.

Puede usar Hola después tooperform de secuencia de comandos de PowerShell esta comprobación manualmente. Implementa Hola por encima de la lógica.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Vínculos relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalación del Agente de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operaciones de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
* [Uso de Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
