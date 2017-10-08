---
title: "aaaManage acceso toocloud aplicaciones mediante la restricción de los inquilinos - Azure | Documentos de Microsoft"
description: "Cómo toouse inquilino restricciones toomanage qué usuarios pueden acceder a las aplicaciones se basa en su inquilino de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Usar aplicaciones de nube de restricciones de inquilino toomanage access tooSaaS

Las organizaciones grandes que resaltan la seguridad desean toomove toocloud servicios como Office 365, pero tooknow necesidad de que los usuarios solo pueden tener acceso a los recursos autorizados. Tradicionalmente, las empresas restringen los nombres de dominio o direcciones IP cuando se quieren tener acceso toomanage. Este enfoque no sirve en un mundo donde las aplicaciones SaaS se hospedan en una nube pública, ejecutándose en nombres de dominio compartidos como outlook.office.com y login.microsoftonline.com. Estas direcciones de bloqueo podría mantener a los usuarios tengan acceso a Outlook en web Hola por completo, en lugar de simplemente limitándolos recursos e identidades de tooapproved.

Desafío de toothis de solución de Azure Active Directory es una característica denominada restricciones de inquilino. Inquilino restricciones habilita las organizaciones toocontrol acceso tooSaaS aplicaciones en la nube, según el uso de las aplicaciones de hello Azure AD inquilino hello para el inicio de sesión único. Por ejemplo, puede que desee aplicaciones de Office 365 tooallow acceso tooyour de la organización, evitando que las instancias de las organizaciones de tooother de acceso de estas mismas aplicaciones.  

Restricciones de inquilinos proporciona las organizaciones Hola capacidad toospecify Hola lista de inquilinos que los usuarios se permiten tooaccess. Azure AD, a continuación, solo concede acceso toothese permitida inquilinos.

En este artículo se centra en las restricciones de inquilinos para Office 365, pero la característica Hola debería funcionar con cualquier aplicación de nube de SaaS que usa los protocolos de autenticación moderna con Azure AD para inicio de sesión único. Si usa aplicaciones con un anuncio de Azure diferente de los inquilinos de inquilino de hello usado por Office 365 de SaaS, asegúrese de que las necesarias se permiten los inquilinos. Para obtener más información acerca de las aplicaciones de nube de SaaS, vea hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Cómo funciona

Hello general solución consta de Hola de los componentes siguientes: 

1. **Azure AD** : si hello `Restrict-Access-To-Tenants: <permitted tenant list>` está presente, Azure AD solo emite tokens de seguridad para hello permiten a los inquilinos. 

2. **Infraestructura de servidor proxy local** : un dispositivo de proxy capaz de inspección de SSL, encabezado de hello tooinsert configurado que contiene la lista de Hola de permite los inquilinos en el tráfico destinado a Azure AD. 

3. **Software de cliente** – toosupport inquilino restricciones, software de cliente debe solicitar tokens directamente de Azure AD, por lo que se puede interceptar el tráfico por la infraestructura del proxy de Hola. Actualmente, cuando se utiliza autenticación moderna (como OAuth 2.0), tanto las aplicaciones de Office 365 basadas en explorador como los clientes de Office admiten Restricciones de inquilino. 

4. **La autenticación moderna** : servicios en la nube deben usar la autenticación moderna toouse inquilino restricciones y bloquear el acceso a los inquilinos de tooall no permitida. Los servicios de Office 365 en la nube deben ser protocolos de autenticación moderna toouse configurado de forma predeterminada. Para información más reciente de hello en Office 365 la compatibilidad con la autenticación moderna, leer [actualizar Office 365 la autenticación moderna](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Hola siguiente diagrama muestra el flujo de tráfico de alto nivel de Hola. Inspección SSL solo se requiere en tráfico tooAzure AD, no toohello servicios de nube de Office 365. Esta distinción es importante porque el volumen de tráfico de Hola para autenticación tooAzure AD está normalmente mucho menor que las aplicaciones de tooSaaS del volumen de tráfico como Exchange Online y SharePoint Online.

![Flujo de tráfico de Restricciones de inquilino: diagrama](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Configuración de Restricciones de inquilino

Hay dos tooget pasos a trabajar con restricciones de inquilino. Hola primer paso es toomake seguro de que los clientes pueden conectarse toohello derecho direcciones. Hola en segundo lugar es tooconfigure la infraestructura del proxy.

### <a name="urls-and-ip-addresses"></a>Direcciones URL e IP reservadas

toouse inquilino restricciones, los clientes deberán ser toohello tooconnect pueda siguiendo las direcciones URL de Azure AD tooauthenticate: login.microsoftonline.com, login.microsoft.com y login.windows.net. Además, tooaccess Office 365, los clientes también deben ser capaz de tooconnect toohello FQDN o direcciones URL y direcciones IP definen en [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Requisitos y configuración de proxy

Hola siguiente configuración es necesario tooenable restricciones de inquilino a través de la infraestructura del proxy. Esta guía es genérica, debe consultar la documentación del proveedor de tooyour proxy para los pasos de implementación específica.

#### <a name="prerequisites"></a>Requisitos previos

- proxy de Hello debe ser tooperform capaz de intercepción de SSL, inserción de encabezado HTTP y destinos de filtro mediante FQDN o direcciones URL. 

- Los clientes deben confiar en la cadena de certificados de hello presentada por el proxy de Hola para las comunicaciones SSL. Por ejemplo, si se usan certificados de una PKI interna, Hola interno emisora raíz certificado de entidad emisora debe ser de confianza.

- Esta característica se incluye en las suscripciones de Office 365, pero si desea que las aplicaciones de SaaS toouse inquilino restricciones toocontrol acceso tooother licencias de Azure AD Premium 1 son necesarios.

#### <a name="configuration"></a>Configuración

Para cada toologin.microsoftonline.com de solicitud entrante, login.microsoft.com y login.windows.net, inserte dos encabezados HTTP: *restringir acceso para inquilinos* y *contexto de restringir acceso*.

encabezados de Hello deben incluir Hola siguientes elementos: 
- Para *restringir acceso para inquilinos*, un valor de \<permiten lista inquilino\>, que es una lista separada por comas de los inquilinos que desea tooallow usuarios tooaccess. Cualquier dominio que está registrado con un inquilino puede ser el inquilino de hello tooidentify usado en esta lista. Por ejemplo, toopermit tener acceso a los inquilinos de Contoso y Fabrikam tooboth, Hola parece de par nombre/valor que:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Para *contexto de restringir acceso*, un valor de un identificador único directorio, declarar qué inquilino es establecer restricciones de inquilino de Hola. Por ejemplo, toodeclare Contoso como inquilino de Hola que establecen Hola directiva de restricciones de inquilino, par de nombre/valor de hello el siguiente aspecto:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Puede encontrar el identificador de directorio en hello [portal de Azure](https://portal.azure.com). Inicie sesión como administrador, seleccione **Azure Active Directory** y luego seleccione **propiedades**.

tooprevent los usuarios insertar su propio encabezado HTTP con los inquilinos no aprobado, Hola necesario proxy encabezado de restringir acceso para inquilinos de hello tooreplace si ya está presente en la solicitud entrante de Hola. 

Los clientes deben estar toouse forzada Hola proxy para todas las solicitudes toologin.microsoftonline.com, login.microsoft.com y login.windows.net. Por ejemplo, si los archivos de PAC usado toodirect clientes toouse Hola proxy, los usuarios finales debe ser capaz de tooedit o deshabilitar archivos Hola PAC.

## <a name="hello-user-experience"></a>experiencia del usuario Hola

Esta sección muestra experiencia de Hola para los usuarios finales y administradores.

### <a name="end-user-experience"></a>Experiencia del usuario final

Un usuario de ejemplo se encuentra en la red de Contoso hello, pero está tratando de instancia de Fabrikam tooaccess Hola un compartido de aplicaciones de SaaS como Outlook en línea. Si Contoso es un inquilino no permitida para esa instancia, el usuario de hello ve Hola después de página:

![Página de acceso denegado para usuarios en inquilinos no permitidos](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Experiencia del administrador

Mientras se realice la configuración de restricciones de inquilino en la infraestructura del proxy corporativo hello, Admins. del puede tener acceso a informes de las restricciones del inquilino de Hola Hola portal de Azure directamente. Hola tooview informes, ir a página de introducción a Azure Active Directory toohello, a continuación, busque en "Otras capacidades".

Hola, Administrador de inquilinos de hello especificado como inquilino de hello contexto de acceso restringido puede usar este toosee informe todos los inicios de sesión bloqueado debido a Hola directiva de restricciones de inquilino, incluida la identidad de hello usa y directorio de destino de Hola por identificador.

![Usar hello Azure tooview portal restringido que intente iniciar sesión](./media/active-directory-tenant-restrictions/portal-report.png)

Al igual que otros informes en hello portal de Azure, puede usar filtros toospecify Hola ámbito del informe. Puede filtrar por un usuario, una aplicación, un cliente o un intervalo de tiempo específico.

## <a name="office-365-support"></a>Compatibilidad con Office 365

Aplicaciones de Office 365 deben cumplir dos criterios toofully soporte inquilino restricciones:

1. cliente Hello utilizado admite la autenticación moderna
2. La autenticación moderna está habilitada como protocolo de autenticación predeterminado de Hola Hola servicio de nube.

Consulte demasiado[actualizar Office 365 la autenticación moderna](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) para obtener información más reciente de hello en qué Office clientes admiten actualmente la autenticación moderna. Esta página también incluye vínculos tooinstructions para habilitar la autenticación moderna de específico Exchange Online y Skype empresarial Online inquilinos. La autenticación moderna ya está habilitada de forma predeterminada en SharePoint Online.

Restricciones de inquilinos es compatible actualmente con las aplicaciones basadas en Explorador de Office 365 (Hola SharePoint de Portal de Office, Yammer, sitios, Outlook en hello Web, etcetera.). Para clientes gruesos (Outlook, Skype Empresarial, Word, Excel, PowerPoint, etc.), Restricciones de inquilinos solo se puede aplicar cuando se usa autenticación moderna.  

Outlook y Skype para los clientes empresariales que admiten la autenticación moderna son todavía puede toouse protocolos heredados en los inquilinos donde no está habilitada la autenticación moderna, omitiendo eficazmente las restricciones del inquilino. Para Outlook en Windows, los clientes pueden elegir restricciones tooimplement impide que los usuarios finales agregar perfiles de tootheir de cuentas de correo electrónico no aprobado. Por ejemplo, vea hello [impedir la adición de cuentas de Exchange no predeterminado](http://gpsearch.azurewebsites.net/default.aspx?ref=1) configuración de directiva de grupo. Para Outlook en plataformas distintas de Windows y para Skype Empresarial en todas las plataformas, actualmente no está disponible la compatibilidad total para restricciones de inquilino.

## <a name="testing"></a>Prueba

Si desea tootry inquilino restricciones antes de implementarlo para toda la organización, hay dos opciones: un enfoque basado en host mediante una herramienta como Fiddler o un lanzamiento por fases de configuración de proxy.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler para un enfoque basado en host

Fiddler es un proxy que se pueden toocapture usado y modifican el tráfico HTTP/HTTPS, incluida la inserción de encabezados HTTP de depuración de web gratuita. tooconfigure Fiddler tootest restricciones de inquilino, lleve a cabo Hola pasos:

1.  [Descargue e instale Fiddler](http://www.telerik.com/fiddler).
2.  Configurar el tráfico HTTPS de Fiddler toodecrypt, por [documentación de Ayuda de Fiddler](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Configurar Hola de Fiddler tooinsert *restringir acceso para inquilinos* y *contexto de restringir acceso* encabezados utilizando reglas personalizadas:
  1. En la herramienta de depurador Web de Fiddler hello, seleccione hello **reglas** menú y seleccione **Personalizar reglas...** archivo de tooopen hello CustomRules.
  2. Agregar Hola siguientes líneas al principio de Hola de hello *OnBeforeRequest* (función). Reemplace \<tenant domain\> por un dominio registrado con el inquilino, por ejemplo, contoso.onmicrosoft.com. Reemplace \<directory ID\> por el identificador GUID de Azure AD del inquilino.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Si necesita tooallow varios inquilinos, use una coma tooseparate Hola inquilino los nombres. Por ejemplo:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Guarde y cierre el archivo de hello CustomRules.

Después de configurar Fiddler, podrá capturar el tráfico por van toohello **archivo** menú y seleccionando **capturar tráfico**.

### <a name="staged-rollout-of-proxy-settings"></a>Lanzamiento por fases de configuración de proxy

Dependiendo de las capacidades de hello de la infraestructura del proxy, es posible que pueda toostage Hola puesta en servicio de los usuarios de tooyour de configuración. Aquí tiene un par de opciones de alto nivel a tener en cuenta:

1.  Usar PAC archivos toopoint prueba usuarios tooa prueba infraestructura del proxy, mientras que los usuarios normales continúan infraestructura del proxy de producción de hello de toouse.
2.  Algunos servidores proxy pueden admitir distintas configuraciones mediante grupos.

Consulte la documentación del servidor de proxy de tooyour para obtener detalles específicos.

## <a name="next-steps"></a>Pasos siguientes

- Lea [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) (Autenticación moderna actualizada de Office 365)

- Hola de revisión [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
