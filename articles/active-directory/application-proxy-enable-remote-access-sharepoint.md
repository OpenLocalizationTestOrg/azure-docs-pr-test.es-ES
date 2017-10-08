---
title: "aaaEnable tooSharePoint de acceso remoto con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Abarca conceptos básicos de hello acerca de cómo toointegrate un servidor de SharePoint local con el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Habilitar acceso remoto tooSharePoint con el Proxy de aplicación de Azure AD

Este artículo se describe cómo toointegrate un servidor de SharePoint local con el Proxy de aplicación de Azure Active Directory (Azure AD).

tooenable tooSharePoint de acceso remoto con el Proxy de aplicación de Azure AD, vea las secciones de hello en este artículo paso a paso.

## <a name="prerequisites"></a>Requisitos previos

En este artículo se da por supuesto que ya tiene SharePoint 2013 o una versión más reciente instalada en su entorno. Además, considere la posibilidad de hello siguiendo los requisitos previos:

* SharePoint incluye compatibilidad nativa con Kerberos. Por lo tanto, los usuarios que obtienen acceso a los sitios internos remotamente a través de Proxy de aplicación de Azure AD pueden asumir toohave experiencia de un inicio de sesión único (SSO).

* Debe toomake unos servidor de SharePoint de tooyour de cambios de configuración. Se recomienda usar un entorno de ensayo. De esta manera, pueda tomar tooyour actualizaciones en primer lugar, el servidor de ensayo y, a continuación, facilitar un ciclo de prueba antes de pasar a producción.

* Se supone que ya configuró SSL para SharePoint, porque se requiere que SSL en hello publicado direcciones URL. Necesita toohave que SSL habilitado en su sitio interno, tooensure que vínculos son enviados/asignada correctamente. Si no configuró SSL, vea [Configure SSL for SharePoint 2013 (Configurar SSL para SharePoint 2013)](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) para obtener instrucciones. Además, asegúrese de que ese certificado Hola de hello conector máquina relaciones de confianza que emite. (certificado de hello no necesita toobe públicamente emitido).

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>Paso 1: Configurar tooSharePoint de inicio de sesión único

Nuestros clientes desean Hola SSO mejor experiencia para sus aplicaciones de back-end, el servidor de SharePoint en este caso. En este escenario habitual de Azure AD, usuario de Hola se autentica una sola vez, porque no se pedirá para la autenticación de nuevo.

Para las aplicaciones locales que requieren o utilizan la autenticación de Windows, puede conseguir SSO mediante una característica denominada delegación limitada de Kerberos (KCD) y el protocolo de autenticación de Kerberos de Hola. KCD, cuando se configura, permite tooobtain de conector de Proxy de aplicación Hola windows vale/símbolo (token) para un usuario, incluso si el usuario de hello no se ha iniciado sesión en tooWindows directamente. toolearn más información acerca de KCD, consulte [introducción de delegación limitada de Kerberos](https://technet.microsoft.com/library/jj553400.aspx).

tooset seguridad KCD para un servidor de SharePoint, usar los procedimientos de Hola Hola siguientes secciones secuenciales:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Asegurarse de que SharePoint se ejecuta como una cuenta de servicio

En primer lugar, asegúrese de que SharePoint se ejecuta bajo una cuenta de servicio definida, no de sistema local, servicio local o servicio de red. Hacer esto para que se pueda adjuntar cuenta válida de tooa de nombres de entidad de seguridad (SPN) de servicio. Los SPN son cómo Hola protocolo Kerberos identifica servicios diferentes. Y se necesita Hola cuenta más adelante tooconfigure Hola KCD.

tooensure que los sitios se ejecutan bajo una cuenta de servicio definido, lleve a cabo Hola pasos:

1. Abra hello **Administración Central de SharePoint 2013** sitio.
2. Vaya demasiado**seguridad** y seleccione **configurar cuentas de servicio**.
3. Seleccione **Grupo de aplicaciones web - SharePoint - 80**. Opciones de Hello pueden diferir ligeramente según Hola nombre del grupo de servidores web, o si hello grupo web utiliza SSL de forma predeterminada.

  ![Opciones para configurar una cuenta de servicio](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Si **seleccionar una cuenta para este componente** es **servicio Local** o **servicio de red**, necesita una cuenta de toocreate. Si no es así, haya terminado y puede mover toohello próxima sección.
5. Haga clic en **Registrar una nueva cuenta administrada**. Después de crear la cuenta, debe establecer **grupo de aplicaciones Web** para poder usar la cuenta de hello.

> [!NOTE]
Necesita toohave un previamente creado la cuenta de Azure AD para servicio de Hola. Se recomienda que permita un cambio de contraseña automático. Para obtener más información sobre el conjunto completo de Hola de pasos y solución de problemas, consulte [configurar el cambio de contraseña automático en SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Configurar SharePoint para Kerberos

Usar KCD tooperform único inicio de sesión toohello servidor de SharePoint, y esto solo funciona con Kerberos.

tooconfigure de sitio de SharePoint para la autenticación Kerberos:

1. Abra hello **Administración Central de SharePoint 2013** sitio.
2. Vaya demasiado**administración de aplicaciones**, seleccione **administrar aplicaciones web**y seleccione el sitio de SharePoint. En este ejemplo, es **SharePoint – 80**.

  ![Seleccionar sitio de SharePoint de Hola](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Haga clic en **proveedores de autenticación** en la barra de herramientas de Hola.
4. Hola **proveedores de autenticación** cuadro, haga clic en **zona predeterminada** configuración de tooview Hola.
5. Hola **Editar autenticación** diálogo cuadro, desplácese hacia abajo hasta que vea **tipos de autenticación de notificaciones** y asegúrese de que ambos **habilitar la autenticación de Windows** y  **Autenticación de Windows integrada** están seleccionadas.
6. En el cuadro de lista desplegable de hello, asegúrese de que **negociar (Kerberos)** está seleccionada.

  ![Cuadro de diálogo Editar autenticación](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Final de Hola de hello **Editar autenticación** cuadro de diálogo, haga clic en **guardar**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Establezca un nombre principal de servicio para hello cuenta de servicio de SharePoint

Antes de configurar Hola KCD, necesita servicio de SharePoint de hello tooidentify ejecuta como cuenta de servicio de Hola que haya configurado. Para ello se establece un SPN. Para obtener más información, consulte [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx) (Nombres de entidad de seguridad de servicio).

formato SPN de Hello es:

```
<service class>/<host>:<port>
```

En formato SPN de hello:

* _clase de servicio_ es un nombre único para el servicio de Hola. Para SharePoint, se usa **HTTP**.

* _host_ es dominio completo de Hola o nombre NetBIOS del host de Hola Hola servicio se está ejecutando. Un sitio de SharePoint, este texto podría tener toobe Hola URL de sitio de hello, según la versión de Hola de IIS que esté usando.

* _port_ es opcional.

Si es el FQDN del servidor de SharePoint de Hola Hola:

```
sharepoint.demo.o365identity.us
```

A continuación, Hola SPN es:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

También podría necesitar tooset SPN para sitios específicos en el servidor. Para más información, vea [Configuración de la autenticación Kerberos](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Preste mucha atención toohello sección "Crear nombres de entidad de servicio para las aplicaciones Web mediante la autenticación Kerberos".

la manera más fácil de Hola para tooset SPN es formatos de SPN de hello toofollow que ya pueden estar presentes para los sitios. Copie los tooregister SPN con la cuenta de servicio de Hola. toodo esto:

1. Examinar el sitio de toohello con hello SPN desde otro equipo.
 Cuando, Hola conjunto relevante de los vales Kerberos se almacena en caché en la máquina de Hola. Estos vales contienen Hola SPN del sitio de destino de Hola que buscó.

2. Puede extraer Hola SPN para ese sitio mediante el uso de una herramienta denominada [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). En una ventana de comandos que se ejecuta en hello mismo contexto que el usuario de Hola que ejecutan el sitio de acceso hello en el Explorador de hello, Hola siguiente comando:
```
Klist
```
Klist, a continuación, devuelve el conjunto de Hola de SPN de destino. En este ejemplo, el valor de hello resaltado es Hola SPN que se necesita:

  ![Resultados del ejemplo de Klist](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Ahora que tienes Hola SPN, debe toomake seguro de que esté configurado correctamente en la cuenta de servicio de Hola que configuró para la aplicación antes de hello web. Ejecute hello siguiente comando desde el símbolo del sistema Hola como un administrador de dominio de hello:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Este comando establece Hola SPN para el servicio de SharePoint de hello cuenta de ejecución como _demo\sp_svc_.

 Reemplace _http/sharepoint.demo.o365identity.us_ con hello SPN para el servidor y _demo\sp_svc_ con la cuenta de servicio de hello en su entorno. Hola Setspn comando busca Hola SPN antes de que agrega. En este caso, es posible que vea un error de **valor SPN duplicado**. Si ve este error, asegúrese de que el valor de hello está asociado con la cuenta de servicio de Hola.

Puede comprobar que Hola que SPN se agregó al ejecutar el comando Setspn de hello con hello -l (opción). toolearn más información acerca de este comando, consulte [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Asegúrese de que dicho conector Hola se establece como un delegado de confianza tooSharePoint

Configurar Hola KCD para que el servicio de Proxy de aplicación de Azure AD de hello puede delegar el servicio de SharePoint de toohello de identidades de usuario. Para ello, habilitar el conector del Proxy de aplicación Hola tooretrieve vales de Kerberos para los usuarios que han sido autenticados en Azure AD. A continuación, ese servidor pasa la aplicación de destino de hello contexto toohello o SharePoint en este caso.

Hola tooconfigure KCD, repita Hola siguiendo los pasos para cada máquina de conector:

1. Inicie sesión como un tooa de administrador de dominio DC y, a continuación, abra **equipos y usuarios de Active Directory**.
2. Buscar equipo Hola que Hola conector se ejecuta en. En este ejemplo, ha Hola mismo servidor de SharePoint.
3. Haga doble clic en el equipo de hello y, a continuación, haga clic en hello **delegación** ficha.
4. Asegúrese de que la configuración de delegación de Hola se establece demasiado**confiar en este equipo para toohello delegación especificado solo servicios**y, a continuación, seleccione **usar cualquier protocolo de autenticación**.

  ![Configuración de delegación](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Haga clic en hello **agregar** botón, haga clic en **usuarios o equipos**y busque la cuenta de servicio de Hola.

  ![Hola agregar SPN para la cuenta de servicio de Hola](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. En lista de Hola de SPN, seleccione Hola uno que creó anteriormente para la cuenta de servicio de Hola.
7. Haga clic en **Aceptar**. Haga clic en **Aceptar** nuevo toosave cambios de Hola.

## <a name="step-2-enable-remote-access-toosharepoint"></a>Paso 2: Habilitar el acceso remoto tooSharePoint

Ahora que ha habilitado SharePoint para Kerberos y configurar KCD, está listo tooset seguridad tooSharePoint de inicio de sesión único. A continuación, desde el conector de hello, puede publicar granja de SharePoint de hello para el acceso remoto a través de Proxy de aplicación de Azure AD.

Hola tooperform siguiendo los pasos, deberá toobe un miembro de función de administrador Global de hello en la cuenta de Azure Active Directory de su organización.

1. Inicie sesión en toohello [portal de Azure](https://manage.windowsazure.com) y busque el inquilino de Azure AD.
2. Haga clic en **Aplicaciones** y luego en **Agregar**.
3. Seleccione **Publicar una aplicación que estará accesible desde fuera de la red**. Si no ve esta opción, asegúrese de que dispone de Azure AD Basic o Premium configurado en el inquilino de Hola.
4. Complete cada una de las opciones de hello como sigue:
 * **Nombre**: use el valor que quiera, por ejemplo **SharePoint**.
 * **Dirección URL interna**: se trata de hello URL del sitio de SharePoint de hello internamente, como **https://SharePoint/**. En este ejemplo, asegúrese de que toouse **https**.
 * **Método de autenticación previa**: seleccione **Azure Active Directory**.

  ![Opciones para agregar una aplicación](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Cuando se publica la aplicación hello, haga clic en hello **configurar** ficha.
6. Desplácese hacia abajo de la opción de toohello **traducir URL en encabezados**. es el valor predeterminado de Hello **Sí**. También cambian**NO**.

 Hola, SharePoint usa _encabezado de Host_ toolook valor sitio Hola. También genera vínculos basándose en este valor. efecto neto de Hello es toomake seguro de que cualquier vínculo que SharePoint genera una dirección URL publicada que se ha configurado correctamente toouse dirección URL externa de Hola. Establecer valor de hello demasiado**Sí** también permite Hola aplicación de conector tooforward hello solicitud toohello back-end. Sin embargo, el valor de hello demasiado**n** decir Hola conector no enviará el nombre de host interno Hola. En su lugar, el conector de hello envía encabezado de host de hello como Hola publicada aplicaciones back-end de toohello de dirección URL.

 Además, tooensure que SharePoint acepta esta dirección URL, debes toocomplete una mayor configuración en el servidor de SharePoint de Hola. Llevará a cabo en la sección siguiente Hola.

7. Cambio **método de autenticación interno** demasiado**autenticación integrada de Windows**. Si su inquilino de Azure AD usa un UPN en la nube de Hola que es diferente de hello UPN local, recuerde tooupdate **delegar la identidad de inicio de sesión** así.
8. Establecer **SPN interno de la aplicación** valor toohello establecidas anteriormente. Por ejemplo, use **http/sharepoint.demo.o365identity.us**.
9. Asignar Hola aplicación tooyour usuarios de destino.

La aplicación debe ser similar toohello siguiente ejemplo:

  ![Aplicación terminada](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Paso 3: Asegurarse de que SharePoint se sabe de dirección URL externa de Hola

El último paso tooensure en la que SharePoint puede encontrar el sitio de hello basado en dirección URL externa de hello, para que representarán los vínculos en función de dicha dirección URL externa. Para ello, mediante la configuración de asignaciones de acceso alternativas para el sitio de SharePoint de Hola.

1. Abra hello **Administración Central de SharePoint 2013** sitio.
2. En **Configuración del sistema**, seleccione **Configurar asignaciones de acceso alternativas**.

 Se abrirá hello **asignaciones alternativas de acceso** cuadro.

  ![Cuadro Asignaciones de acceso alternativas](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. En la lista desplegable situada al lado de hello **la colección de asignaciones de acceso alternativas**, seleccione **colección de la asignación de acceso alternativas de cambio**.
4. Seleccione el sitio, por ejemplo **SharePoint - 80**.

  ![Selección de un sitio](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Puede elegir tooadd Hola publicado direcciones URL como una dirección URL interna o una dirección URL pública. Este ejemplo utiliza una dirección URL pública como Hola extranet.
6. Haga clic en **editar direcciones URL públicas** en hello **Extranet** ruta de acceso y, a continuación, escriba ruta de acceso Hola Hola publicó la aplicación, como en el paso anterior de Hola. Por ejemplo, escriba **https://sharepoint-iddemo.msappproxy.net**.

  ![Escriba la ruta de acceso de Hola](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Haga clic en **Guardar**.

 Ahora puede tener acceso a sitio de SharePoint de hello externamente a través de Proxy de aplicación de Azure AD.

## <a name="next-steps"></a>Pasos siguientes

- [Cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md)
- [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
- [Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/) (Publicación de SharePoint 2016 y Office Online Server con el proxy de aplicación de Azure AD)
