---
title: "Active Directory Domain Services: Implementación del proxy de aplicación de Azure Active Directory | Microsoft Docs"
description: "En este artículo se explica cómo usar el proxy de aplicación en dominios administrados de Azure Active Directory Domain Services."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Implementación del proxy de aplicación de Azure AD en dominios administrados de Azure Active Directory Domain Services.
Proxy de aplicación de Azure Active Directory (AD) le ayuda a los trabajadores remotos mediante la publicación de toobe de aplicaciones local tiene acceso a través de hello internet. Con los servicios de dominio de Active Directory de Azure, puede ahora elevación y-desplazamiento aplicaciones heredadas ejecuta Servicios de infraestructura de tooAzure locales. A continuación, puede publicar dichas aplicaciones usan Hola Proxy de aplicación de Azure AD, tooprovide toousers de acceso remoto seguro en su organización.

Si le toohello nuevo Proxy de aplicación de Azure AD, obtener más información acerca de esta característica con hello artículo siguiente: [cómo tooprovide el acceso remoto a aplicaciones locales de tooon](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Antes de empezar
tareas de hello tooperform enumeradas en este artículo, necesita:

1. Una **suscripción de Azure**válida.
2. Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.
3. Un **licencia de Azure AD Basic y Premium** es necesario toouse Hola Proxy de aplicación de Azure AD.
4. **Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD. Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Tarea 1: Habilitar el proxy de aplicación de Azure AD en su directorio de Azure AD
Realizar Hola siguiendo los pasos tooenable Hola Proxy de aplicación de Azure AD para su directorio Azure AD.

1. Inicie sesión como administrador en hello [portal de Azure](http://portal.azure.com).

2. Haga clic en **Azure Active Directory** toobring una introducción a directory Hola. Haga clic en **Aplicaciones empresariales**.

    ![Selección de un directorio de Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. Haga clic en **Proxy de aplicación**. Si no tiene una suscripción de Azure AD Basic y Azure AD Premium, verá un tooenable opción una versión de prueba. Alternar **habilitar Proxy de aplicación?** demasiado**habilitar** y haga clic en **guardar**.

    ![Habilitación del proxy de aplicación](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload Hola conector, haga clic en hello **conector** botón.

    ![Descarga del conector](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. En la página de descarga de hello, acepte los términos de licencia de Hola y el acuerdo de privacidad y haga clic en hello **descargar** botón.

    ![Confirmación de la descarga](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Tarea 2: aprovisionar Unidos a un dominio Windows servidores toodeploy hello Azure AD aplicación conector del Proxy
Debe tener Unidos a un dominio Windows Server virtual máquinas en el que puede instalar el conector del Proxy de aplicación de Azure AD Hola. Función de las aplicaciones de Hola que se está publicadas, puede elegir tooprovision varios servidores en el que está instalado el conector de Hola. Esta opción de implementación ofrece mayor disponibilidad y lo ayuda a administrar cargas de autenticación más intensas.

Aprovisionar servidores del conector de hello en Hola misma red virtual (o una red virtual conectado/emparejar), en la que ha habilitado el dominio administrado de los servicios de dominio de AD de Azure. De forma similar, los servidores de hello hospedar aplicaciones Hola publicar a través de Proxy de aplicación Hola necesitan toobe instalado en hello misma red virtual de Azure.

servidores del conector tooprovision, realice las tareas de Hola que se describen en el artículo de hello titulado [unirse a un dominio administrado de Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Tarea 3: instalar y registrar Hola conector del Proxy de aplicación de Azure AD
Anteriormente, se aprovisiona una máquina virtual de Windows Server y Unidos a un dominio administrado toohello. En esta tarea, instalará el conector del Proxy de aplicación de Azure AD de hello en esta máquina virtual.

1. Copiar en el que se instala el conector de Proxy de aplicación Web de Azure AD de Hola Hola conector instalación paquete toohello VM.

2. Ejecutar **AADApplicationProxyConnectorInstaller.exe** en la máquina virtual de Hola. Acepte los términos de licencia del software de Hola.

    ![Aceptación de los términos de instalación](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Durante la instalación, son tooregister solicitadas Hola conector con hello Proxy de aplicación de su directorio Azure AD.
    * Proporcione sus **credenciales de administrador global de Azure AD**. Su inquilino de administrador global puede ser diferente de sus credenciales de Microsoft Azure.
    * Hello administrador cuenta usada tooregister Hola conector debe pertenecer toohello mismo directorio donde haya habilitado servicio de Proxy de aplicación Hola. Por ejemplo, si el dominio del inquilino de hello es contoso.com, Hola, administrador debe ser admin@contoso.com o cualquier otro alias válido en ese dominio.
    * Si la configuración de seguridad mejorada de Internet Explorer está activado para el servidor de Hola donde va a instalar el conector de hello, pantalla de bienvenida registro podría bloquearse. acceso de tooallow, siga las instrucciones de hello en el mensaje de error de saludo. Asegúrese de que Internet Explorer Enhanced Security está desactivado.
    * Si el registro del conector no funciona, consulte [Solucionar problemas de Proxy de aplicación](../active-directory/active-directory-application-proxy-troubleshoot.md).

    ![Conector instalado](./media/app-proxy/app-proxy-connector-installed.png)
4. Conector de hello tooensure funciona correctamente, ejecución Hola Solucionador de problemas de conector de Proxy Azure aplicación de AD. Debería ver un informe correcto después de solucionador de problemas de ejecución Hola.

    ![Mensaje del Solucionador de problemas que todo está correcto](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Debería ver el conector de hello recién instalado aparece en la página de proxy de aplicación hello en su directorio Azure AD.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> Puede elegir tooinstall conectores en varios servidores tooguarantee alta disponibilidad para la autenticación de las aplicaciones publicadas a través de hello Proxy de aplicación de Azure AD. Realizar Hola mismos pasos enumerados anteriormente tooinstall conector de hello en otro servidores tooyour Unidos a un dominio de administrado.
>
>

## <a name="next-steps"></a>Pasos siguientes
Se configurado Hola Proxy de aplicación de Azure AD y se integra con el dominio administrado de los servicios de dominio de AD de Azure.

* **Migrar las máquinas virtuales de tooAzure de aplicaciones:** puede elevación y desplazamiento de las aplicaciones locales servidores máquinas virtuales tooAzure tooyour Unidos a un dominio administrado. Si lo hace, le ayuda a evitar los costos de infraestructura de Hola de servidores locales.

* **Publicar aplicaciones mediante el Proxy de aplicación de Azure AD:** publicar aplicaciones que se ejecutan en máquinas virtuales de Azure con hello Proxy de aplicación de Azure AD. Para obtener más información, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](../active-directory/application-proxy-publish-azure-portal.md).


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Nota de implementación: publique las aplicaciones de IWA (autenticación integrada) mediante el proxy de aplicación de Azure AD.
Permitir que las aplicaciones de tooyour de inicio de sesión único mediante la autenticación de Windows integrada (IWA) mediante la concesión de permiso de conectores Proxy de aplicación tooimpersonate los usuarios y enviar y recibir tokens en su nombre. Configurar la delegación limitada de kerberos (KCD) para hello conector toogrant Hola requerido permisos tooaccess recursos en el dominio administrado Hola. Usar el mecanismo KCD de basada en recursos de hello en dominios administrados para aumentar la seguridad.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Habilitar la delegación restringida de kerberos basada en recursos para el conector del Proxy de aplicación de hello Azure AD
Conector de Proxy de aplicación de Azure Hola debe configurarse para la delegación limitada de kerberos (KCD), por lo que puede suplantar a usuarios en el dominio administrado Hola. En un dominio administrado de Azure AD Domain Services, no tiene privilegios de administrador de dominios. Por lo tanto, **la KCD tradicional de nivel de cuenta no se puede configurar en un dominio administrado**.

En su lugar, use la que está basada en recursos, como se describe en este [artículo](active-directory-ds-enable-kcd.md).

> [!NOTE]
> Necesita toobe un miembro del grupo de 'Administradores de controlador de dominio de AAD' hello, tooadminister Hola administrados mediante cmdlets de AD PowerShell del dominio.
>
>

Usar la configuración de Hola de hello Get-ADComputer PowerShell cmdlet tooretrieve para equipo de hello en qué Hola Proxy de aplicación de Azure AD está instalado el conector.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Por lo tanto, utilice tooset de cmdlet Set-ADComputer Hola seguridad basada en recursos KCD para servidor de recursos de Hola.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Si ha implementado varios conectores de Proxy de aplicación en el dominio administrado, deberá tooconfigure KCD basada en recursos para cada instancia de conector de este tipo.


## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Configuración de la delegación restringida de kerberos en un dominio administrado](active-directory-ds-enable-kcd.md)
* [Introducción a la delegación limitada de kerberos](https://technet.microsoft.com/library/jj553400.aspx)
