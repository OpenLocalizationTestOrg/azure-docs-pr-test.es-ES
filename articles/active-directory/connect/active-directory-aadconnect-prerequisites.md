---
title: 'Azure AD Connect: Requisitos previos y hardware | Microsoft Docs'
description: En este tema se describe los requisitos previos de Hola y requisitos de hardware de Hola para Azure AD Connect
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Requisitos previos de Azure AD Connect
Este tema describe los requisitos previos de Hola y requisitos de hardware de Hola para Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Antes de instalar Azure AD Connect
Antes de instalar Azure AD Connect, hay algunas cosas que necesita.

### <a name="azure-ad"></a>Azure AD
* Una suscripción de Azure o una [suscripción de prueba de Azure](https://azure.microsoft.com/pricing/free-trial/). Esta suscripción solo es necesario para tener acceso a Hola portal de Azure y no para usar Azure AD Connect. Si utilizas Office 365 o PowerShell, no es necesario un toouse de suscripción de Azure Connect de Azure AD. Si tiene una licencia de Office 365, también puede usar el portal de Office 365 Hola. Con una licencia de Office 365 pagada, también puede obtener en hello portal de Azure desde el portal de Office 365 Hola.
  * También puede usar hello [portal de Azure](https://portal.azure.com). Este portal no requiere una licencia de Azure AD.
* [Agregar y comprobar el dominio de hello](../active-directory-domains-add-azure-portal.md) piensa toouse en Azure AD. Por ejemplo, si planear toouse contoso.com para los usuarios, asegúrese de que este dominio se ha comprobado y no se usa solo dominio predeterminado de hello contoso.onmicrosoft.com.
* Un inquilino de Azure AD permite de forma predeterminada objetos de 50 k. Al comprobar el dominio, el límite de hello es mayor too300k objetos. Si necesita incluso más objetos en Azure AD, deberá tooopen un límite de soporte técnico toohave mayúsculas Hola aumenta aún más. Si necesita más de 500 000 objetos, necesitará una licencia como Office 365, Azure AD Basic, Azure AD Premium o Enterprise Mobility and Security.

### <a name="prepare-your-on-premises-data"></a>Preparación de los datos locales
* Use [IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify errores como duplicados y problemas de formato en el directorio antes de sincronizar tooAzure AD y Office 365.
* Revise [las características de sincronización opcionales que se pueden habilitar en Azure AD](active-directory-aadconnectsyncservice-features.md) y valore cuáles son las que debe habilitar.

### <a name="on-premises-active-directory"></a>Active Directory local
* Hola AD versión y el bosque nivel funcional del esquema debe ser Windows Server 2003 o posterior. controladores de dominio de Hello pueden ejecutar cualquier versión siempre que cumplan los requisitos de nivel de hello esquema y el bosque.
* Si tiene previsto característica de hello toouse **escritura diferida de contraseñas**, a continuación, debe ser controladores de dominio de hello en Windows Server 2008 (con Service Pack más reciente) o una versión posterior. Si los controladores de dominio están en 2008 (antes de la versión R2), también debe aplicar la [revisión KB2386717](http://support.microsoft.com/kb/2386717).
* controlador de dominio de Hello usado por Azure AD debe ser grabable. Es **no admite** toouse un RODC (controlador de dominio de solo lectura) y Azure AD Connect no siga cualquier escribir redirecciones.
* Es **no admite** toouse bosques o dominios con dominios de segundo nivel (dominios de etiqueta única) locales.
* Es **no admite** toouse con "dotted" bosques o dominios locales (nombre contiene un punto ".") Nombres NetBios.
* Se recomienda demasiado[habilitar Papelera de reciclaje de Active Directory de hello](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Servidor de Azure AD Connect
* Azure AD Connect no puede instalarse en Small Business Server o Windows Server Essentials. Hola servidor debe usar Windows Server estándar o superior.
* servidor de Connect de Hello Azure AD debe tener una GUI completa instalada. Es **no admite** tooinstall en server core.
* Azure AD Connect debe instalarse en Windows Server 2008 o en una versión superior. Este servidor puede ser un controlador de dominio o un servidor miembro si usa la configuración rápida. Si usa una configuración personalizada, servidor hello también puede ser independiente y no tiene toobe tooa Unidos a un dominio.
* Si instalar Azure AD Connect en Windows Server 2008 o Windows Server 2008 R2, asegúrese de que tooapply hello las revisiones más recientes desde Windows Update. instalación de Hello no es capaz de toostart con un servidor de revisiones.
* Si tiene previsto característica de hello toouse **la sincronización de contraseña**, debe ser el servidor de hello Azure AD Connect en Windows Server 2008 R2 SP1 o posterior.
* Si tiene previsto toouse una **cuenta de servicio administrada de grupo**, a continuación, debe ser el servidor de hello Azure AD Connect en Windows Server 2012 o posterior.
* Hola AD Azure Connect servidor debe tener [.NET Framework 4.5.1](#component-prerequisites) o una versión posterior y [Microsoft PowerShell 3.0](#component-prerequisites) o posterior instalado.
* servidor de Azure AD Connect Hello no debe tener la directiva de grupo de transcripción de PowerShell habilitada.
* Si se va a implementar los servicios de federación de Active Directory, los servidores de Hola donde se instala AD FS o Proxy de aplicación Web deben ser Windows Server 2012 R2 o posterior. [Administración remota de Windows](#windows-remote-management) debe estar habilitada en estos servidores para la instalación remota.
* Si se implementa Servicios de federación de Active Directory, necesita [Certificados SSL](#ssl-certificate-requirements).
* Si se va a implementar los servicios de federación de Active Directory, deberá tooconfigure [la resolución de nombres](#name-resolution-for-federation-servers).
* Si los administradores globales tienen MFA habilitado, a continuación, Hola URL **https://secure.aadcdn.microsoftonline-p.com** debe estar en la lista de sitios de confianza de Hola. Son solicitada tooadd esta lista de sitios de confianza toohello del sitio cuando se le pida un desafío MFA y no se ha agregado antes. Puede usar Internet Explorer tooadd tooyour sitios de confianza.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server usado por Azure AD Connect
* Azure AD Connect requiere un datos de identidad de toostore de base de datos de SQL Server. De forma predeterminada, se instala SQL Server 2012 Express LocalDB (versión ligera de SQL Server Express). SQL Server Express tiene un límite de tamaño de 10GB que permite toomanage aproximadamente 100.000 objetos. Si necesita toomanage un mayor volumen de objetos de directorio, deberá toopoint Hola instalación Asistente tooa instalación distinta de SQL Server.
* Si utiliza una instancia de SQL Server independiente, se aplican estos requisitos:
  * Connect de Azure AD admite todos los tipos de Microsoft SQL Server desde SQL Server 2008 (con Service Pack más reciente) tooSQL Server 2016 SP1. **No se admite** Base de datos SQL de Microsoft Azure como base de datos.
  * Debe usar una intercalación de SQL sin distinción de mayúsculas y minúsculas. Estas intercalaciones se identifican porque el nombre incluye \_CI_. Es **no admite** toouse una intercalación que distingue mayúsculas de minúsculas, identificado por \_CS_ en su nombre.
  * Solo se puede tener un motor de sincronización por cada instancia de SQL. Es **no admite** tooshare SQL instancia mediante la sincronización de FIM o MIM, DirSync o sincronización de Azure AD.

### <a name="accounts"></a>Cuentas
* Una cuenta de administrador Global de Azure AD para el inquilino de hello Azure AD desea toointegrate con. Debe tratarse de una **cuenta profesional o educativa** y no puede ser una **cuenta Microsoft**.
* Si usa la configuración rápida o actualiza desde DirSync, debe tener una cuenta de administrador de empresa para su instancia de Active Directory local.
* [Cuentas en Active Directory](active-directory-aadconnect-accounts-permissions.md) si utiliza la ruta de instalación de una configuración personalizada de Hola.

### <a name="connectivity"></a>Conectividad
* servidor de Connect de Hello Azure AD necesita resolución de DNS de intranet e internet. Hello servidor DNS debe ser capaz de tooresolve nombres tooyour locales de Active Directory y Hola extremos de Azure AD.
* Si tiene servidores de seguridad de la Intranet y necesita tooopen puertos entre servidores de hello Azure AD Connect y los controladores de dominio, consulte [Azure AD Connect puertos](active-directory-aadconnect-ports.md) para obtener más información.
* Si el límite de servidor proxy o firewall que pueden tener acceso a las direcciones URL, a continuación, Hola direcciones URL que se documentan en [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) debe abrirse.
  * Si utilizas Hola Microsoft Cloud en Alemania u Hola nube de Microsoft Azure Government, consulte [consideraciones de instancias de servicio de sincronización de Azure AD Connect](active-directory-aadconnect-instances.md) para las direcciones URL.
* Azure AD Connect es usar TLS 1.0 toocommunicate con Azure AD de forma predeterminada. Puede cambiar este tooTLS 1.2 siguiendo los pasos de hello en [habilitar TLS 1.2 para Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* Si está utilizando un proxy de salida para la conexión toohello Internet, Hola después configuración Hola **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** archivo debe agregarse para el Asistente para la instalación de Hola y Azure AD Connect sync toobe tooconnect pueda toohello Internet y Azure AD. Este texto se debe especificar al final de hello del archivo de Hola. En este código, &lt;PROXYADRESS&gt; representa Hola nombre de host o dirección IP real del proxy.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Si el servidor proxy requiere autenticación y, a continuación, hello [cuenta de servicio](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) debe estar ubicado en hello dominio y se debe usar toospecify de ruta de acceso de instalación de hello personalizado configuración un [cuenta de servicio personalizado](active-directory-aadconnect-get-started-custom.md#install-required-components). También necesita un toomachine.config diferentes de cambios. Con este cambio en el archivo machine.config, motor de asistente y sincronización de la instalación de hello responder las solicitudes de tooauthentication desde el servidor de proxy de Hola. En todas las páginas del Asistente de instalación, excepto hello **configurar** página Hola iniciado sesión del usuario se usan las credenciales. En hello **configurar** página Hola final del Asistente para instalación de hello, contexto de hello es conmutada toohello [cuenta de servicio](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) creada por el usuario. sección de Hello machine.config debería tener este aspecto.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Cuando Azure AD Connect envía una tooAzure de solicitud web AD como parte de la sincronización de directorios, Azure AD puede tardar hasta too5 minutos toorespond. Es común para la configuración de tiempo de espera de inactividad de conexión de proxy servidores toohave. Asegúrese de Hola se ha configurado tooat menos de 6 minutos o más.

Para obtener más información, vea MSDN sobre hello [proxy elemento predeterminado](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Para obtener más información si tiene problemas de conectividad, consulte [Solución de problemas de conectividad](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Otros
* Opcional: Una prueba usuario tooverify sincronización de cuentas.

## <a name="component-prerequisites"></a>Requisitos previos de los componentes
### <a name="powershell-and-net-framework"></a>PowerShell y .NET Framework
Azure AD Connect depende de Microsoft PowerShell y .NET Framework 4.5.1. Necesita que esta versión o una posterior esté instalada en el servidor. Dependiendo de la versión de Windows Server, Hola siguientes:

* Windows Server 2012R2
  * Microsoft PowerShell se instala de forma predeterminada, no se requiere ninguna acción.
  * .NET Framework 4.5.1 y versiones posteriores se ofrecen mediante Windows Update. Asegúrese de que ha instalado tooWindows de las actualizaciones más recientes de hello servidor en el Panel de Control de Hola.
* Windows Server 2008R2 y Windows Server 2012
  * Hola versión más reciente de PowerShell de Microsoft está disponible en **Windows Management Framework 4.0**, está disponible en [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 y versiones posteriores están disponibles en el [Centro de descarga de Microsoft](http://www.microsoft.com/downloads).
* Windows Server 2008
  * Hola admitido la última versión de PowerShell está disponible en **Windows Management Framework 3.0**, está disponible en [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 y versiones posteriores están disponibles en el [Centro de descarga de Microsoft](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Habilitación de TLS 1.2 en Azure AD Connect
Azure AD Connect usa TLS 1.0 de forma predeterminada para cifrar la comunicación de hello entre el servidor de motor de sincronización de Hola y Azure AD. Puede cambiar esto configurando toouse de aplicaciones .net TLS 1.2 de forma predeterminada en el servidor de Hola. Puede encontrar más información sobre TLS 1.2 en [Documento informativo sobre seguridad de Microsoft 2960358 ](https://technet.microsoft.com/security/advisory/2960358).

1. No se puede habilitar TLS 1.2 en Windows Server 2008. Se requiere Windows Server 2008 R2 o posterior. Asegúrese de que tiene la revisión de .net 4.5.1 Hola instalada para su sistema operativo, consulte [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358). Puede que ya tenga esta revisión o una posterior instalada en el servidor.
2. Si usa Windows Server 2008 R2, asegúrese de que TLS 1.2 esté habilitado. En el servidor de Windows Server 2012 y versiones posteriores, TLS 1.2 ya debe estar habilitado.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Para todos los sistemas operativos, establecer esta clave del registro y reinicie el servidor de Hola.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Si también desea tooenable 1.2 de TLS entre el servidor de motor de sincronización de Hola y un servidor SQL remoto, asegúrese de que tiene instaladas para versiones de hello necesario [soporte de TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Requisitos previos para la instalación y la configuración de la federación
### <a name="windows-remote-management"></a>Administración remota de Windows
Cuando se usa Azure AD Connect toodeploy los servicios de federación de Active Directory o hello Proxy de aplicación Web, compruebe estos requisitos:

* Si el servidor de destino de hello está unido al dominio, a continuación, asegúrese de que administrados remotos de Windows está habilitado
  * En una ventana de comandos PSH con privilegios elevados, use el comando `Enable-PSRemoting –force`
* Si el servidor de destino de hello es un elemento que no es de dominio unido a la máquina WAP, a continuación, hay un par de requisitos adicionales
  * En la máquina de destino de hello (máquina WAP):
    * Asegúrese de hello winrm (administración remota de Windows / WS-Management) está ejecutando el servicio mediante el complemento Servicios de Hola
    * En una ventana de comandos PSH con privilegios elevados, use el comando `Enable-PSRemoting –force`
  * En el equipo de hello en qué Hola asistente está ejecutando (si el equipo de destino hello es no es de dominio no es de confianza o Unidos a un dominio):
    * En una ventana de comandos PSH con privilegios elevados, use el comando de Hola`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * En el Administrador de servidores:
      * Agregar grupo de toomachine de host de red Perimetral WAP (el administrador del servidor -> Administrar -> Agregar servidores... usar la pestaña DNS)
      * Pestaña de administrador del servidor todos los servidores: haga clic con el servidor WAP y elija administrar como..., escriba credenciales local (no de dominio) para la máquina WAP Hola
      * toovalidate PSH la conectividad remota, en la pestaña de administrador del servidor todos los servidores de hello: haga clic en el servidor WAP y elija Windows PowerShell. Debe abrir una sesión remota de PSH se pueden establecer sesiones de PowerShell remotas tooensure.

### <a name="ssl-certificate-requirements"></a>Requisitos del certificado SSL
* Se recomienda encarecidamente toouse Hola mismo certificado SSL a través de todos los nodos de la granja de servidores de AD FS y todos los servidores proxy de aplicación Web.
* certificado de Hello debe ser un X509 certificado.
* Puede usar un certificado autofirmado en servidores de federación en un entorno de laboratorio de pruebas. Sin embargo, para un entorno de producción, se recomienda que obtengan certificados de Hola de una entidad de certificación pública.
  * Si usa un certificado que no sea de confianza pública, asegúrese de que ese certificado Hola instalado en cada servidor Proxy de aplicación Web es de confianza en ambas servidor local de Hola y en todos los servidores de federación
* identidad de Hello del certificado de hello debe coincidir con nombre de servicio de federación de hello (por ejemplo, sts.contoso.com).
  * identidad de Hello es una extensión de nombre alternativo (SAN) de asunto de tipo dNSName o, si no hay entradas SAN, el nombre del firmante de hello especificado como un nombre común.  
  * Varias entradas de SAN pueden estar presentes en el certificado de hello, proporcionado por uno de ellos coincide con el nombre de servicio de federación de Hola.
  * Si tiene previsto toouse al área de trabajo, un SAN adicional es necesario con el valor de hello **enterpriseregistration.** seguido por el sufijo de nombre Principal de usuario (UPN) de Hola de su organización, por ejemplo, **enterpriseregistration.contoso.com**.
* No se admiten certificados basados en claves CryptoAPI Next Generation (CNG) ni en proveedores de almacenamiento de claves. Esto significa que debe utilizar un certificado basado en un CSP (proveedor de servicios criptográficos) y no en un KSP (proveedor de almacenamiento de claves).
* Se admiten certificados comodín.

### <a name="name-resolution-for-federation-servers"></a>Resolución de nombres para los servidores de federación
* Configurar registros DNS para hello el nombre de servicio de federación de AD FS (por ejemplo sts.contoso.com) de intranet (el servidor DNS interno) de Hola y Hola extranet (públicas de DNS a través de su registrador de dominios). Registro de DNS de intranet de hello, asegúrese de que usa un registros y no los registros CNAME. Esto es necesario para toowork de autenticación de windows correctamente desde el equipo Unidos a un dominio.
* Si va a implementar más de un servidor de AD FS o servidor Proxy de aplicación Web, asegúrese de que ha configurado el equilibrador de carga y que el equilibrador de carga de registros DNS de hello para el servicio de federación de hello AD FS nombre (por ejemplo sts.contoso.com) punto toohello.
* Para toowork de la autenticación integrada de windows para las aplicaciones de explorador mediante Internet Explorer en la intranet, asegúrese de que Hola nombre de servicio de federación de AD FS (por ejemplo sts.contoso.com) se agrega toohello la zona de intranet en Internet Explorer. Esto puede controlarse a través de directiva de grupo y tooall implementado los equipos unidos su dominio.

## <a name="azure-ad-connect-supporting-components"></a>Componentes de soporte de Azure AD Connect
Hola aquí te mostramos una lista de componentes que instala Azure AD Connect en servidor hello donde está instalado Azure AD Connect. Esta lista es para una instalación rápida básica. Si elige toouse otro SQL Server en hello instale la página de servicios de sincronización y, a continuación, SQL Express LocalDB no está instalado localmente.

* Azure AD Connect Health
* Microsoft Online Services - Ayudante para el inicio de sesión, para profesionales de TI (instalado pero sin ninguna dependencia)
* Utilidades de línea de comandos de Microsoft SQL Server 2012
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Paquete de redistribución de Microsoft Visual C++ 2013

## <a name="hardware-requirements-for-azure-ad-connect"></a>Requisitos de hardware de Azure AD Connect
tabla de Hello siguiente muestra los requisitos mínimos de hello para el equipo de sincronización de Azure AD Connect Hola.

| Cantidad de objetos en Active Directory | CPU | Memoria | Tamaño de disco duro |
| --- | --- | --- | --- |
| Menos de 10.000 |1,6 GHz |4 GB |70 GB |
| 10.000–50.000 |1,6 GHz |4 GB |70 GB |
| 50.000–100.000 |1,6 GHz |16 GB |100 GB |
| De 100.000 o más objetos se requiere la versión completa de Hola de SQL Server | | | |
| 100.000–300.000 |1,6 GHz |32 GB |< 300 GB |
| 300.000–600.000 |1,6 GHz |32 GB |450 GB |
| Más de 600.000 |1,6 GHz |32 GB |500 GB |

Hola requisitos mínimos para equipos que ejecutan AD FS o servidores de aplicaciones Web es la siguiente de hello:

* CPU: 1,6 GHz con doble núcleo o superior
* MEMORIA: 2 GB o superior
* VM de Azure: configuración A2 o superior

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
