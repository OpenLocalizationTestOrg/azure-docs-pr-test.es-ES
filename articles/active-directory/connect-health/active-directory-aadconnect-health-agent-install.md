---
title: "instalación de agente Connect Health aaaAzure AD | Documentos de Microsoft"
description: "Se trata de una página de Azure AD Connect Health Hola que describe la instalación de agentes de Hola para AD FS y sincronización."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Instalación del agente de Azure AD Connect Health
Este documento le guía a través de la instalación y configuración de agentes de mantenimiento de hello Azure AD Connect. Puede descargar agentes Hola de [aquí](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Requisitos
Hello en la tabla siguiente es una lista de los requisitos para usar Azure AD Connect Health.

| Requisito | Description |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health es una característica de Azure AD Premium y, por tanto, requiere Azure AD Premium. </br></br>Para más información, consulte [Introducción a Azure Active Directory Premium](../active-directory-get-started-premium.md). </br>toostart una prueba gratuita de 30 días, vea [iniciar una prueba.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Debe ser un global inicia el Administrador de su tooget de Azure AD con Azure AD Connect Health |De forma predeterminada, sólo los administradores globales Hola pueden instalar y configurar Hola mantenimiento agentes tooget iniciado, portal de Hola de acceso y realizar las operaciones dentro de Azure AD Connect Health. Para más información, consulte [Administración del directorio de Azure AD](../active-directory-administer.md). <br><br> Mediante el Control de acceso basado en roles puede permitir el acceso a los usuarios de tooAzure AD Connect Health tooother en su organización. Para más información, consulte cómo usar el [control de acceso basado en rol para Azure AD Connect Health](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control). </br></br>**Importante:** Hola cuenta utilizada durante la instalación de agentes de hello debe ser una cuenta profesional o educativa. No puede ser una cuenta Microsoft. Para más información, consulte [Inicio de sesión en Azure como una organización](../sign-up-organization.md). |
| El agente de Azure AD Connect Health está instalado en cada servidor de destino. | Azure AD Connect Health requiere Hola agentes de mantenimiento toobe instalado y configurado en los datos de servidores de destino tooreceive hello y proporciona capacidades de supervisión y análisis de Hola </br></br>Por ejemplo, datos de tooget de la infraestructura de AD FS, el agente de Hola deben instalarse en hello AD FS y servidores Proxy de aplicación Web. De forma similar, los datos de tooget en sus instalaciones de infraestructura de AD DS, Hola agente debe instalarse en controladores de dominio de Hola. </br></br> |
| Puntos de conexión de servicio de Azure de conectividad saliente toohello | Durante la instalación y en tiempo de ejecución, el agente de hello requiere extremos de servicio de conectividad tooAzure AD Connect Health. Si conectividad saliente está bloqueado mediante Firewalls, asegúrese de que Hola siguiendo los puntos de conexión se agregan toohello lista de elementos permitido: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Puerto: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Conectividad saliente basada en direcciones IP | Para la dirección IP basada en dirección filtrado en los firewalls, consulte toohello [intervalos de direcciones IP de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| La inspección de SSL para el tráfico saliente se filtra o se deshabilita. | Hola agente registro paso o datos de las operaciones de carga pueden producir un error si se produce la inspección de SSL o finalización para el tráfico saliente en la capa de red Hola. |
| Puertos del Firewall de servidor hello ejecutando el agente de Hola. |agente de Hello requiere Hola después de puertos de firewall toobe para abrir Hola agente toocommunicate a extremos de servicio de mantenimiento de Azure AD de Hola.</br></br><li>Puerto TCP 443</li><li>Puerto TCP 5671</li> |
| Permitir Hola después de sitios Web si está habilitada la seguridad mejorada de Internet Explorer |Si está habilitada la seguridad mejorada de Internet Explorer, a continuación, hello siguientes sitios Web debe permitirse en servidor hello que va toohave Hola agente instalado.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>servidor de federación de Hola para su organización de confianza para Azure Active Directory. Por ejemplo: https://sts.contoso.com</li> |
|Deshabilitar FIPS|FIPS no es compatible con los agentes de Azure AD Connect Health.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Instalar agente de Azure AD Connect Health para AD FS Hola
toostart Hola instalación del agente, haga doble clic en el archivo .exe de Hola que ha descargado. En la primera pantalla de bienvenida, haga clic en instalar.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Una vez finalizada la instalación de hello, haga clic en configurar ahora.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Esto inicia un proceso de registro de agente de PowerShell ventana tooinitiate Hola. Cuando se le solicite, inicie sesión con una cuenta de Azure AD que tenga acceso tooperform el registro del agente. De forma predeterminada Hola cuenta de administrador Global tiene acceso.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Después de iniciar sesión, PowerShell continuará. Una vez que se complete, puede cerrar PowerShell y configuración de hello está completa.

En este momento, hello agente de servicios deben ser iniciado automáticamente permitiendo Hola agente carga Hola necesario datos toohello en la nube servicio de forma segura.

Si no se cumplen todos los requisitos previos de Hola que se describen en las secciones anteriores hello, aparecen mensajes de advertencia en la ventana de PowerShell de hello. Estar seguro de hello toocomplete [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) antes de instalar el agente de Hola. Hola siguiente captura de pantalla es un ejemplo de estos errores.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

se ha instalado el agente de hello tooverify, busque Hola después de servicios en el servidor de Hola. Si completó la configuración de hello, ya deben ejecutarse. En caso contrario, se detienen hasta que se complete la configuración de Hola.

* Servicio de diagnóstico de AD FS de Azure AD Connect Health
* Servicio de análisis de AD FS de Azure AD Connect Health
* Servicio de supervisión de AD FS de Azure AD Connect Health

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Instalación del agente en servidores de Windows Server 2008 R2
En el caso de los servidores de Windows Server 2008 R2, realice los siguientes pasos:

1. Asegúrese de que ese servidor hello ejecuta Service Pack 1 o superior.
2. Desactive ESC de Internet Explorer para la instalación del agente:
3. Instale Windows PowerShell 4.0 en cada uno de los servidores de hello antes de instalar Hola agente AD Health. tooinstall Windows PowerShell 4.0:
   * Instalar [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) con hello después instalador sin conexión de vínculo toodownload Hola.
   * Instale PowerShell ISE (desde Características de Windows)
   * Instalar hello [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Instale Internet Explorer versión 10 o posterior en el servidor de Hola. (Requiere tooauthenticate de servicio de mantenimiento de hello, con sus credenciales de administrador de Azure).
4. Para obtener más información acerca de cómo instalar Windows PowerShell 4.0 en Windows Server 2008 R2, consulte el artículo de wiki de hello [aquí](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Habilitación de la auditoría de AD FS
> [!NOTE]
> Esta sección solo aplica a servidores de tooAD FS. No es necesario toofollow estos pasos en los servidores de Proxy de aplicación Web de Hola.
>

En orden para hello toogather de características de análisis de uso y analizar datos, Hola agente de Azure AD Connect Health necesitan Hola información en los registros de auditoría de hello AD FS. que no están habilitados de forma predeterminada. Hola de uso después de la auditoría de procedimientos tooenable AD FS y toolocate Hola AD FS registros de auditoría, en los servidores de AD FS.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable auditoría de AD FS en Windows Server 2008 R2
1. Haga clic en **iniciar**, seleccione demasiado**programas**, seleccione demasiado**herramientas administrativas**y, a continuación, haga clic en **directiva de seguridad Local**.
2. Navegue toohello **administración de derechos de seguridad de configuración de seguridad\Directivas locales\Asignación** carpeta y, a continuación, haga doble clic en generar auditorías de seguridad.
3. En hello **configuración de seguridad Local** , compruebe que se muestra la cuenta de servicio de hello AD FS 2.0. Si no está presente, haga clic en **Agregar usuario o grupo** y agregarlo a toohello lista y, a continuación, haga clic en **Aceptar**.
4. tooenable auditoría, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando de hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Cierre Directiva de seguridad Local y, a continuación, abrir el complemento Administración de Hola. Hola tooopen complemento de administración, haga clic en **iniciar**, seleccione demasiado**programas**, seleccione demasiado**herramientas administrativas**y, a continuación, haga clic en AD administración de ADFS 2.0.
6. En el panel de acciones de hello, haga clic en Editar propiedades del servicio de federación.
7. Hola **propiedades del servicio de federación** diálogo cuadro, haga clic en hello **eventos** ficha.
8. Seleccione hello **auditorías de aciertos** y **auditorías de errores** casillas de verificación.
9. Haga clic en **Aceptar**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable auditoría de AD FS en Windows Server 2012 R2
1. Abra **directiva de seguridad Local** abriendo **el administrador del servidor** en pantalla de inicio de hello, o un administrador del servidor en la barra de tareas de hello en el escritorio de hello, a continuación, haga clic en **herramientas locales, directiva de seguridad**.
2. Navegue toohello **seguridad de configuración de seguridad\Directivas Locales\asignación de derechos** carpeta y, a continuación, haga doble clic en **generar auditorías de seguridad**.
3. En hello **configuración de seguridad Local** , compruebe que se muestra la cuenta de servicio de hello AD FS. Si no está presente, haga clic en **Agregar usuario o grupo** y agregarlo a toohello lista y, a continuación, haga clic en **Aceptar**.
4. tooenable auditoría, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando de hello: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Cerrar **directiva de seguridad Local**y, a continuación, abra hello **administración de AD FS** complemento (en el administrador del servidor, haga clic en herramientas y, a continuación, seleccione Administración de AD FS).
6. En el panel de acciones de hello, haga clic en **editar propiedades del servicio de federación**.
7. En el cuadro de diálogo de propiedades del servicio de federación de hello, haga clic en hello **eventos** ficha.
8. Seleccione hello **auditorías de aciertos y auditorías de errores** casillas de verificación y, a continuación, haga clic en **Aceptar**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable auditoría de AD FS en Windows Server 2016
1. Abra **directiva de seguridad Local** abriendo **el administrador del servidor** en pantalla de inicio de hello, o un administrador del servidor en la barra de tareas de hello en el escritorio de hello, a continuación, haga clic en **herramientas locales, directiva de seguridad**.
2. Navegue toohello **seguridad de configuración de seguridad\Directivas Locales\asignación de derechos** carpeta y, a continuación, haga doble clic en **generar auditorías de seguridad**.
3. En hello **configuración de seguridad Local** , compruebe que se muestra la cuenta de servicio de hello AD FS. Si no está presente, haga clic en **Agregar usuario o grupo** y agregar la lista de toohello de cuentas de servicio de hello AD FS y, a continuación, haga clic en **Aceptar**.
4. tooenable auditoría, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando de hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Cerrar **directiva de seguridad Local**y, a continuación, abra hello **administración de AD FS** complemento (en el administrador del servidor, haga clic en herramientas y, a continuación, seleccione Administración de AD FS).
6. En el panel de acciones de hello, haga clic en **editar propiedades del servicio de federación**.
7. En el cuadro de diálogo de propiedades del servicio de federación de hello, haga clic en hello **eventos** ficha.
8. Seleccione hello **auditorías de aciertos y auditorías de errores** casillas de verificación y, a continuación, haga clic en **Aceptar**. Esto se debe habilitar de forma predeterminada.
9. Abra una ventana de PowerShell y ejecute el siguiente comando de hello: ```Set-AdfsProperties -AuditLevel Verbose```.

Tenga en cuenta que el nivel de auditoría "básico" está habilitado de forma predeterminada. Obtener más información acerca de hello [mejora de la auditoría de AD FS en Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>registros de auditoría de hello toolocate AD FS
1. Abra **Visor de eventos**.
2. Vaya tooWindows registros y seleccione **seguridad**.
3. En hello derecho, haga clic en **filtrar registro actual**.
4. En Origen de evento, seleccione **Auditoría de AD FS**.

![Registros de auditoría de AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Una directiva de grupo puede deshabilitar la auditoría de AD FS. Si se deshabilita la auditoría de AD FS, no estará disponible el análisis de uso sobre las actividades de inicio de sesión. Asegúrese de no tener ninguna directiva de grupo de este tipo.
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>Instalar agente de Azure AD Connect Health hello para la sincronización
agente de Hello Azure AD Connect Health para la sincronización se instala automáticamente en la compilación más reciente de Hola de Azure AD Connect. toouse Azure AD Connect para la sincronización, se necesita la versión más reciente de hello toodownload de Azure AD Connect e instalarlo. Puede descargar la versión más reciente de hello [aquí](http://www.microsoft.com/download/details.aspx?id=47594).

se ha instalado el agente de hello tooverify, busque Hola después de servicios en el servidor de Hola. Si completó la configuración de hello, ya deben ejecutarse. En caso contrario, se detienen hasta que se complete la configuración de Hola.

* Servicio de análisis de sincronización de Azure AD Connect Health
* Servicio de supervisión de sincronización de Azure AD Connect Health

![Comprobación de Azure AD Connect Health para sincronización](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Recuerde que el uso de Azure AD Connect Health requiere Azure AD Premium. Si no tiene Azure AD Premium, son toocomplete no se puede configuración de Hola Hola portal de Azure. Para obtener más información, vea hello [página requisitos](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Registro manual de Azure AD Connect Health para sincronización
Si hello Azure AD Connect Health para el registro del agente de sincronización se produce un error después de instalar correctamente Azure AD Connect, puede usar Hola siguiente comando de PowerShell toomanually registrar el agente de Hola.

> [!IMPORTANT]
> Con este comando de PowerShell solo es necesario si se produce un error en el registro del agente Hola después de instalar Azure AD Connect.
>
>

Hello siguiente es el comando requiere PowerShell solo al registro del agente de mantenimiento de Hola se produce un error incluso después de una instalación correcta y la configuración de Azure AD Connect. Servicios de Azure AD Connect Health Hola se iniciarán después de que se ha registrado correctamente el agente de Hola.

Puede registrar manualmente el agente de hello Azure AD Connect Health para sincronizar con el siguiente comando de PowerShell de hello:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

comando de Hello toma siguientes parámetros:

* AttributeFiltering: $true (valor predeterminado): si Azure AD Connect no está sincronizando el conjunto de atributos predeterminados de Hola y ha personalizado toouse un atributo de filtro establecido. $false en caso contrario.
* StagingMode: $false (valor predeterminado): si servidor de Azure AD Connect hello no está en modo, $true de ensayo si servidor hello es configurar toobe en modo de almacenamiento provisional.

Cuando se le solicite para la autenticación debe usar Hola la misma cuenta de administrador global (como admin@domain.onmicrosoft.com) que se usó para configurar Azure AD Connect.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Instalar agente de Azure AD Connect Health para AD DS Hola
toostart Hola instalación del agente, haga doble clic en el archivo .exe de Hola que ha descargado. En la primera pantalla de bienvenida, haga clic en instalar.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Una vez finalizada la instalación de hello, haga clic en configurar ahora.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Con esto se iniciará un símbolo del sistema seguido de una instancia de PowerShell que ejecutará Register-AzureADConnectHealthADDSAgent. Cuando toosign solicitada en tooAzure, continúe e inicie sesión.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Después de iniciar sesión, PowerShell continuará. Una vez que se complete, puede cerrar PowerShell y configuración de hello está completa.

En este momento, los servicios de hello deben iniciarse automáticamente permitiendo Hola agente toomonitor y recopilan datos. Si no se cumplen todos los requisitos previos de Hola que se describen en las secciones anteriores hello, aparecen mensajes de advertencia en la ventana de PowerShell de hello. Estar seguro de hello toocomplete [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) antes de instalar el agente de Hola. Hola siguiente captura de pantalla es un ejemplo de estos errores.

![Comprobación de Azure AD Connect Health para AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

se ha instalado el agente de hello tooverify, busque Hola después de servicios en el controlador de dominio de Hola.

* Servicio de análisis de AD DS de Azure AD Connect Health
* Servicio de supervisión de AD DS de Azure AD Connect Health

Si completó la configuración de hello, estos servicios ya deberían estar ejecutándose. En caso contrario, se detienen hasta que se complete la configuración de Hola.

![Comprobación de Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Registro del agente con PowerShell
Después de instalar Hola agente adecuado setup.exe, puede realizar el paso de registro del agente hello mediante Hola siga los comandos de PowerShell según el rol de Hola. Abra una ventana de PowerShell y ejecute el comando apropiado de hello:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Estos comandos aceptan "Credential" como un registro de hello toocomplete de parámetro de una manera no interactiva o en un equipo de Server Core.
* Hola credencial se puede capturar en una variable de PowerShell que se pasa como un parámetro.
* Puede proporcionar cualquier identidad de AD de Azure que tiene acceso tooregister Hola agentes y no tiene MFA habilitado.
* De forma predeterminada los administradores globales tienen acceso tooperform el registro del agente. También puede permitir que otros menos tooperform de identidades con privilegios este paso. Más información sobre el [control de acceso basado en rol](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Configurar agentes de Azure AD Connect Health toouse HTTP Proxy
Puede configurar agentes de Azure AD Connect Health toowork con un HTTP Proxy.

> [!NOTE]
> * No se admite el uso de "Netsh WinHttp set ProxyServerAddress" como agente de hello usa las solicitudes web de System.Net toomake en lugar de los servicios HTTP de Microsoft Windows.
> * Hola dirección de Http Proxy configurada es usado toopass-a través de Https mensajes cifrados.
> * No se admiten los servidores proxy autenticados (mediante HTTPBasic).
>
>

### <a name="change-health-agent-proxy-configuration"></a>Cambio de configuración del proxy del agente de estado
Tener Hola después de conectar el agente de mantenimiento toouse un HTTP Proxy de opciones tooconfigure Azure AD.

> [!NOTE]
> Deben reiniciar todos los servicios de agente de Azure AD Connect Health, en orden para toobe de configuración de proxy de hello actualizado. Ejecute el siguiente comando de hello:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Importación de configuración de proxy existente
##### <a name="import-from-internet-explorer"></a>Importación desde Internet Explorer.
Configuración del proxy HTTP de Internet Explorer puede importarse, toobe utilizan Hola agentes de Azure AD Connect Health. En cada uno de los servidores de hello ejecutando el agente de mantenimiento de hello, ejecute hello siguiente comando de PowerShell:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importación desde WinHTTP
Se puede importar la configuración del proxy WinHTTP, toobe utilizan Hola agentes de Azure AD Connect Health. En cada uno de los servidores de hello ejecutando el agente de mantenimiento de hello, ejecute hello siguiente comando de PowerShell:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Especificación manual de direcciones de proxy
Puede especificar manualmente un servidor proxy en cada uno de los servidores de hello ejecutando Hola agente de mantenimiento, ejecutando el siguiente comando de PowerShell de hello:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Ejemplo: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myservidorproxy: 443*

* "address" puede ser un nombre de servidor resoluble DNS o una dirección IPv4
* "port" se puede omitir. Si se omite, se elige 443 como puerto predeterminado.

#### <a name="clear-existing-proxy-configuration"></a>Borrado de la configuración de proxy existente
Puede desactivar la configuración de proxy existente Hola ejecutando el siguiente comando de hello:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Lectura de la configuración de proxy actual
Puede leer la configuración de proxy de hello configurado actualmente ejecutando el siguiente comando de hello:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Probar conectividad tooAzure AD servicio Connect Health
Es posible que pueden surgir problemas originados por agente de Azure AD Connect Health hello toolose conectividad con el servicio de estado de conexión de hello Azure AD. problemas de red, problemas de permisos o de otro tipo.

Si agente hello es servicio de no se puede toosend datos toohello Azure AD Connect Health durante más de dos horas, se indica con hello después de alerta en el portal de hello: "los datos de servicio de mantenimiento no están una toodate". Puede confirmar si agente de Azure AD Connect Health Hola afectado es servicio de tooupload capaz de datos toohello Azure AD Connect Health ejecutando el siguiente comando de PowerShell de hello:

    Test-AzureADConnectHealthConnectivity -Role ADFS

parámetro de función Hello actualmente toma Hola siguientes valores:

* ADFS
* Sync
* ADDS

Puede usar hello - ShowResults marca en hello comando tooview registros detallados. Utilice el siguiente ejemplo de Hola:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> herramienta de conectividad de hello toouse, debe primer registro del agente se Hola completa. Si no es capaz de toocomplete el registro del agente hello, asegúrese de que se cumplen todos los hello [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) de Azure AD Connect Health. Esta prueba de conectividad se realiza de forma predeterminada durante el registro del agente.
>
>

## <a name="related-links"></a>Vínculos relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Operaciones de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
* [Uso de Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md)
* [Preguntas más frecuentes de Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
