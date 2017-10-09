---
title: aaaMFA servidor con AD FS en Windows Server | Documentos de Microsoft
description: "Este artículo describe cómo tooget a trabajar con la autenticación multifactor Azure y AD FS en Windows Server 2012 R2 y 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Configurar toowork de servidor Azure Multi-factor Authentication con AD FS en Windows Server
Si utiliza los servicios de federación de Active Directory (AD FS) y desea toosecure los recursos de nube o local, puede configurar toowork servidor Azure Multi-factor Authentication con AD FS. Esta configuración desencadena la verificación en dos pasos para los puntos de conexión de alto valor.

En este artículo se describe el uso del Servidor Azure Multi-Factor Authentication con AD FS en Windows Server 2012 R2 y Windows Server 2016. Para obtener más información, lea acerca de cómo demasiado[proteger recursos de nube y locales mediante servidor Azure Multi-factor Authentication con AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Protección de Windows Server AD FS con Servidor Azure Multi-Factor Authentication
Cuando se instala el servidor de autenticación multifactor de Azure, deberá Hola siguientes opciones:

* Instalar servidor de autenticación multifactor de Azure localmente en hello mismo servidor que AD FS
* Instalar a adaptador de la autenticación multifactor Azure Hola localmente en hello servidor de AD FS y, a continuación, instalar el servidor de autenticación multifactor en un equipo diferente

Antes de comenzar, tenga en cuenta de hello siguiente información:

* No son necesario tooinstall servidor Azure Multi-factor Authentication en el servidor de AD FS. Sin embargo, debe instalar el adaptador de la autenticación multifactor de Hola para AD FS en un Windows Server 2012 R2 o Windows Server 2016 que ejecuta AD FS. Puede instalar a servidor hello en un equipo diferente si es una versión admitida e instala Hola adaptador de AD FS por separado en el servidor de federación de AD FS. Vea Hola siguiendo los procedimientos toolearn cómo tooinstall Hola adaptador por separado.
* Si su organización está usando métodos de comprobación de la aplicación móvil o de mensaje de texto, las cadenas de hello definidas en la configuración de la empresa contienen un marcador de posición, <$*application_name*$>. En la versión 7.1 del Servidor MFA, puede especificar el nombre de aplicación que reemplazará este marcador de posición. En v7.0 o anterior, este marcador de posición no se sustituye automáticamente cuando se usa el adaptador de hello AD FS. Para esas versiones anteriores, quitar marcador de posición de Hola de cadenas adecuadas Hola si se protege AD FS.
* cuenta de Hello que usan toosign en debe tener grupos de seguridad de toocreate de derechos de usuario en el servicio de Active Directory.
* Asistente para la instalación de adaptador de Hola la autenticación multifactor AD FS crea un grupo de seguridad denominado PhoneFactor Admins en la instancia de Active Directory. A continuación, agrega la cuenta de servicio de AD FS Hola de su grupo de toothis de servicio de federación. Compruebe que en el controlador de dominio que hello al grupo PhoneFactor Admins se haya creado y que la cuenta de servicio de hello AD FS es un miembro de este grupo. Si es necesario, agregue manualmente toohello de cuenta de servicio de hello AD FS al grupo PhoneFactor Admins en el controlador de dominio.
* Para obtener información acerca de cómo instalar Hola SDK del servicio Web con el portal de usuarios de hello, que conozca [implementar el portal de usuarios de hello para el servidor de autenticación multifactor de Azure.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Instalar a servidor de autenticación multifactor de Azure localmente en el servidor de AD FS Hola
1. Descargue e instale Servidor Azure Multi-Factor Authentication en el servidor de AD FS. Para obtener información sobre la instalación, consulte la [introducción a Servidor Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
2. En la consola de administración de servidor de autenticación multifactor de Azure de hello, haga clic en hello **AD FS** icono. Seleccionar opciones de hello **permitir la inscripción de usuario** y **permitir que los usuarios tooselect método**.
3. Seleccione las opciones adicionales que le gustaría tener toospecify en su organización.
4. Haga clic en **Instalar adaptador de AD FS**.
   
   <center>![Nube](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Si se muestra la ventana de Active Directory de hello, significa que dos cosas. El equipo está tooa Unidos a un dominio y configuración de Active Directory de Hola para proteger la comunicación entre el adaptador de hello AD FS y servicio de la autenticación multifactor de hello está incompleta. Haga clic en **siguiente** tooautomatically completar esta configuración, o seleccione hello **Omitir configuración automática de Active Directory y configurarlo manualmente** casilla de verificación. Haga clic en **Siguiente**.
6. Si se muestra ventanas de grupo Local de hello, significa que dos cosas. El equipo no está tooa Unidos a un dominio y configuración de grupo local de Hola para proteger la comunicación entre el adaptador de hello AD FS y servicio de la autenticación multifactor de hello está incompleta. Haga clic en **siguiente** tooautomatically completar esta configuración, o seleccione hello **Omitir configuración automática de grupo Local y configurarlo manualmente** casilla de verificación. Haga clic en **Siguiente**.
7. En el Asistente para la instalación de hello, haga clic en **siguiente**. Servidor de autenticación multifactor Azure crea Hola al grupo PhoneFactor Admins y agrega toohello de cuenta de servicio de hello AD FS al grupo PhoneFactor Admins.
   <center>![Nube](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. En hello **iniciar instalador** página, haga clic en **siguiente**.
9. En el instalador del adaptador Hola la autenticación multifactor AD FS, haga clic en **siguiente**.
10. Haga clic en **cerrar** cuando finalice la instalación de Hola.
11. Cuando se haya instalado el adaptador de hello, debe registrarlo con AD FS. Abra Windows PowerShell y ejecute el siguiente comando de hello:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Nube](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse el adaptador recién registrado, Editar directiva de autenticación global de hello en AD FS. En la consola de administración de hello AD FS, vaya toohello **las directivas de autenticación** nodo. Hola **la autenticación multifactor** sección, haga clic en hello **editar** vínculo siguiente toohello **configuración Global** sección. Hola **Editar directiva de autenticación Global** ventana, seleccione **la autenticación multifactor** como método de autenticación adicional y, a continuación, haga clic en **Aceptar**. Hola adaptador está registrado como WindowsAzureMultiFactorAuthentication. Reiniciar servicio de hello AD FS para el efecto de tootake de registro de hello.

<center>![Nube](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

En este momento, servidor de autenticación multifactor es configurar toobe una toouse de proveedor de autenticación adicional con AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Instalar una instancia independiente de adaptador de AD FS hello mediante Hola SDK del servicio Web
1. Instale Hola SDK del servicio Web en servidor de Hola que está ejecutando el servidor de autenticación multifactor.
2. Siguiente de hello copia archivos de hello \Program Files\Multi-Factor Authentication Server toohello de directorio en el que piensa que el adaptador de tooinstall Hola AD FS:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Ejecute el archivo de instalación de archivos MultiFactorAuthenticationAdfsAdapterSetup64.msi de Hola.
4. En el instalador del adaptador Hola la autenticación multifactor AD FS, haga clic en **siguiente** instalación de hello toostart.
5. Haga clic en **cerrar** cuando finalice la instalación de Hola.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Editar archivo de hello MultiFactorAuthenticationAdfsAdapter.config
Siga estos archivos de pasos tooedit Hola MultiFactorAuthenticationAdfsAdapter.config:

1. Conjunto hello **usewebservicesdk como** nodo demasiado**true**.  
2. Establecer el valor de Hola de **WebServiceSdkUrl** toohello URL de hello Web servicio SDK de Multi-factor Authentication. Por ejemplo: *https://contoso.com/&lt;nombrecertificado&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, donde *certificatename* es Hola nombre del certificado.  
3. Editar script de Hola Register-MultiFactorAuthenticationAdfsAdapter.ps1 agregando *- ConfigurationFilePath &lt;ruta de acceso&gt;*  toohello final de hello `Register-AdfsAuthenticationProvider` comando, donde  *&lt;ruta de acceso&gt;*  es el archivo de MultiFactorAuthenticationAdfsAdapter.config de toohello de ruta de acceso completa de Hola.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Configurar Hola SDK del servicio Web con un nombre de usuario y una contraseña
Hay dos opciones para configurar Hola SDK del servicio Web. Hola en primer lugar es con un nombre de usuario y una contraseña, sino Hola en segundo lugar con un certificado de cliente. Siga estos pasos para la primera opción de Hola o pase de hello en segundo lugar.  

1. Establecer el valor de Hola de **WebServiceSdkUsername** tooan cuenta que sea miembro del grupo de seguridad PhoneFactor Admins Hola. Hola de uso &lt;dominio&gt;&#92;&lt; nombre de usuario&gt; formato.  
2. Establecer el valor de Hola de **WebServiceSdkPassword** toohello contraseña de cuenta correspondiente.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Configurar Hola SDK del servicio Web con un certificado de cliente
Si no desea toouse un nombre de usuario y una contraseña, siga estos Hola de tooconfigure pasos SDK del servicio Web con un certificado de cliente.

1. Obtener un certificado de cliente de una entidad de certificación de servidor hello que ejecuta Hola SDK del servicio Web. Obtenga información acerca de cómo demasiado[obtener certificados de cliente](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importación Hola cliente certificado toohello ordenador almacén de certificados personales en servidor hello que está ejecutando Hola SDK del servicio Web. Asegúrese de que el certificado público que Hola entidad emisora de certificados está en el almacén de certificados de certificados raíz de confianza.  
3. Exportar claves públicas y privadas de Hola Hola cliente tooa .pfx del archivo de certificado.  
4. Exportar la clave pública de hello en el archivo .cer de Base64 formato tooa.  
5. En el administrador del servidor, compruebe que esta característica de autenticación de asignaciones de certificado de cliente hello \Web Server\Security\IIS de servidor Web (IIS) está instalada. Si no está instalado, seleccione **agregar Roles y características** tooadd esta característica.  
6. En el Administrador de IIS, haga doble clic en **Editor de configuración de** en el sitio Web de Hola que contiene el directorio virtual del SDK del servicio Web de Hola. Es importante tooselect Hola sitio Web no directorio virtual Hola.  
7. Vaya toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** sección.  
8. Configure enabled demasiado**true**.  
9. Establezca onetoonecertificatemappingsenabled como demasiado**true**.  
10. Haga clic en hello **...**  toooneToOneMappings siguiente y, a continuación, haga clic en hello **agregar** vínculo.  
11. Abra el archivo .cer Hola codificado en Base64 que exportó anteriormente. Quite *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* y todos los saltos de línea. Copie la cadena resultante Hola.  
12. Conjunto de la cadena de toohello certificado copiada en hello anterior paso.  
13. Configure enabled demasiado**true**.  
14. Establecer la cuenta de tooan de nombre de usuario que sea miembro del grupo de seguridad PhoneFactor Admins Hola. Hola de uso &lt;dominio&gt;&#92;&lt; nombre de usuario&gt; formato.  
15. Establecer contraseña de cuenta correspondiente de hello contraseña toohello y, a continuación, cierre el Editor de configuración.  
16. Haga clic en hello **aplicar** vínculo.  
17. En el directorio virtual del SDK del servicio Web de hello, haga doble clic en **autenticación**.  
18. Compruebe que suplantación de ASP.NET y la autenticación básica se establecen demasiado**habilitado**, y que todos los demás elementos se establecen demasiado**deshabilitado**.  
19. En el directorio virtual del SDK del servicio Web de hello, haga doble clic en **configuración de SSL**.  
20. Configurar certificados de cliente demasiado**Accept**y, a continuación, haga clic en **aplicar**.  
21. Copie Hola .pfx exportado server toohello anterior que se está ejecutando Hola adaptador de AD FS.  
22. Importe el almacén de certificados personales de hello .pfx archivo toohello equipo local.  
23. Haga clic en y seleccione **administrar claves privadas**y, a continuación, conceder acceso de lectura toohello cuenta usó toosign en el servicio de toohello AD FS.  
24. Abra Hola cliente certificado y copia Hola la huella digital de hello **detalles** ficha.  
25. En el archivo MultiFactorAuthenticationAdfsAdapter.config de hello, establezca **WebServiceSdkCertificateThumbprint** toohello cadena copió en el paso anterior de Hola.  

Por último, tooregister Hola adaptador, ejecute hello \Program Files\Multi-script Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1 en PowerShell. Hola adaptador está registrado como WindowsAzureMultiFactorAuthentication. Reiniciar servicio de hello AD FS para el efecto de tootake de registro de hello.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Protección de los recursos de Azure AD mediante AD FS
toosecure el recurso en la nube, configure una regla de notificaciones para que los servicios de federación de Active Directory emite hello multipleauthn notificación cuando un usuario realiza la verificación en dos pasos correctamente. Esta notificación se pasa en tooAzure AD. Siga este toowalk procedimiento a través de los pasos de hello:

1. Abra Administración de AD FS.
2. Hola izquierda, seleccione **Veracidades**.
3. Haga clic con el botón derecho en **Plataforma de identidad de Microsoft Office 365** y seleccione **Editar reglas de notificaciones…**

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. En Reglas de transformación de emisión, haga clic en **Agregar regla**.

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. En Hola transformar notificaciones Asistente para agregar reglas, seleccione **paso a través o filtrar una notificación entrante** de Hola lista desplegable y haga clic en **siguiente**.

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Asigne un nombre a la regla.
7. Seleccione **referencias de métodos de autenticación** tipo de notificación de Hola entrantes.
8. Seleccione **Pasar a través todos los valores de notificaciones**.
    ![Asistente para agregar regla de notificación de transformación](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Haga clic en **Finalizar** Cierre la consola de administración FS Hola AD.

## <a name="related-topics"></a>Temas relacionados
Para Ayuda para solucionar problemas, vea hello [preguntas más frecuentes de Azure Multi-factor Authentication](multi-factor-authentication-faq.md)
