---
title: "aaaVPN integración con Azure MFA con la extensión NPS | Documentos de Microsoft"
description: "Este artículo describe la integración de la infraestructura VPN con Azure MFA con la extensión de servidor de directivas de redes (NPS) de Hola para Microsoft Azure."
services: active-directory
keywords: "Azure MFA, integración de VPN, Azure Active Directory, extensión Servidor de directivas de redes"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>Integrar la infraestructura VPN con Azure Multi-factor Authentication (MFA) con la extensión de servidor de directivas de redes (NPS) de Hola para Azure

## <a name="overview"></a>Información general

Hola extensión de servicio de directivas de redes (NPS) de Azure permite a las organizaciones toosafeguard autenticación de cliente de servicio de autenticación remota telefónica de usuario (RADIUS) mediante basada en la nube [Azure la autenticación multifactor (MFA)](multi-factor-authentication-get-started-server-rdg.md), que proporciona una comprobación de dos pasos.

Este artículo proporciona instrucciones para integrar la infraestructura de hello NPS con Azure MFA con extensión NPS de Hola para Azure tooenable segura verificacion para los usuarios que intenten tooconnect tooyour red mediante una VPN. 

Hola servicios de acceso (NPS) y directivas de redes proporciona las organizaciones Hola siguientes capacidades:

* Especificar ubicaciones centrales para la administración de Hola y control de toospecify de las solicitudes de red que se puede conectar, qué horas del día en que se permiten las conexiones, duración de Hola de las conexiones y el nivel de Hola de seguridad que los clientes deben usar tooconnect y así sucesivamente. En vez de especificar estas directivas en cada VPN o servidor de puerta de enlace de Escritorio remoto (RD), estas directivas se especifican una vez en una ubicación central. se utiliza el protocolo RADIUS Hola Hola tooprovide centralizada de autenticación, autorización y contabilidad (AAA). 
* Establecer y aplicar directivas de mantenimiento de cliente de protección de acceso a redes (NAP) que determinan si los dispositivos se conceden acceso restringido o sin restricción toonetwork recursos.
* Proporcione un medio tooenforce autenticación y autorización para conmutadores Ethernet y puntos de acceso inalámbricos compatibles con too802.1x de acceso.    

Consulte [Servidor de directivas de redes (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top) para más información. 

seguridad de tooenhance y proporcionar alto nivel de cumplimiento, las organizaciones pueden integrar NPS con tooensure de MFA de Azure que los usuarios utilicen verificacion toobe capaz de conectarse toohello puerto virtual en el servidor VPN de Hola. Para los usuarios toobe concedido acceso, deberán proporcionar su combinación de nombre de usuario/contraseña con la información que Hola usuario tiene en su control. Esta información debe ser de confianza y no duplicable fácilmente, como un número de teléfono móvil, el número fijo o una aplicación en un dispositivo móvil, entre otros.

Disponibilidad de toohello anteriores de hello extensión NPS para Azure, los clientes que deseaban tooimplement verificacion de integran NPS y los entornos de Azure MFA tenían tooconfigure y mantienen un servidor independiente de MFA en el entorno local de hello como se documentan en la puerta de enlace de escritorio remoto y servidor de Azure Multi-factor Authentication con RADIUS.

disponibilidad de Hola de extensión NPS de Hola para Azure le proporciona las organizaciones Hola elección toodeploy una solución MFA basándose en local o una autenticación de cliente RADIUS de basado en la nube MFA solución toosecure.
 
## <a name="authentication-flow"></a>Flujo de autenticación
Cuando un usuario conecta tooa puerto virtual en un servidor VPN, deben autenticarse primero con una variedad de protocolos, lo que permite el uso de Hola de una combinación de nombre de usuario/contraseña y métodos de autenticación basada en certificados. 

En suma tooauthenticating y verificación de identidad, los usuarios deben tener Hola los permisos de acceso telefónico adecuados. En implementaciones sencillas, se establecen estos permisos de acceso telefónico que permiten tener acceso directamente en los objetos de usuario de Active Directory de Hola. 

 ![Propiedades de usuario](./media/nps-extension-vpn/image1.png)

Para implementaciones sencillas, cada servidor VPN concede o deniega el acceso en función de las directivas definidas en cada servidor VPN local.

En las implementaciones más grandes y más escalables, Hola directivas que conceder o denegar el acceso a VPN están centralizados en servidores RADIUS. En este caso, el servidor VPN de Hola actúa como un servidor de acceso (cliente RADIUS) que reenvía las solicitudes de conexión y el servidor RADIUS de cuenta mensajes tooa. tooconnect toohello puerto virtual en el servidor VPN de hello, los usuarios deben autenticarse y cumplen condiciones Hola definidas de forma centralizada en los servidores RADIUS. 

Cuando Hola extensión NPS para Azure está integrado con hello NPS, flujo de autenticación correcta de hello es el siguiente:

1. servidor VPN de Hello recibe una solicitud de autenticación de un usuario VPN que incluya Hola username y password tooconnect tooa recurso, como una sesión de escritorio remoto. 
2. Actúa como cliente RADIUS, servidor VPN convierte el mensaje de solicitud de acceso RADIUS de hello solicitud tooa y envía mensajes de Hola (la contraseña se cifra) servidor RADIUS (NPS) de toohello donde está instalado Hola extensión NPS. 
3. Hola nombre de usuario y se compruebe la combinación de contraseña en Active Directory. Si Hola nombre de usuario / contraseña es incorrecta, Hola servidor RADIUS envía un mensaje de rechazo de acceso. 
4. Si todas las condiciones que se especifican en Hola de solicitud de conexión de NPS y se cumplen las directivas de red (por ejemplo, la hora del día o de grupo restricciones de pertenencia), Hola extensión NPS desencadena una solicitud de autenticación secundaria con Azure MFA. 
5. MFA de Azure se comunica con Azure Active Directory, recupera los detalles de usuario de Hola y realiza la autenticación secundaria de hello mediante método hello configurado por el usuario de hello (mensaje de texto, aplicación móvil etc.). 
6. Cuando se realiza correctamente de hello desafío MFA, MFA de Azure se comunica extensión de hello resultado toohello NPS.
7. Después de intento de conexión de Hola se autentica y se autoriza, el servidor NPS de Hola donde se instala la extensión de hello envía un aceptación de acceso RADIUS mensaje toohello servidor VPN (cliente RADIUS).
8. usuario de Hola se concede acceso toohello puerto virtual en el servidor VPN y establece un túnel VPN cifrado.

## <a name="prerequisites"></a>Requisitos previos
En esta sección se detalla los requisitos previos de hello necesarios antes de integrar Azure MFA con hello puerta de enlace de escritorio remoto. Antes de comenzar, debe tener Hola siguiendo los requisitos previos en su lugar.

* Infraestructura de VPN
* Directiva de red y rol de servicios de acceso (NPS)
* Licencia de Azure MFA
* Software de Windows Server
* Bibliotecas
* Azure AD sincronizado con AD local 
* Identificador de GUID de Azure Active Directory

### <a name="vpn-infrastructure"></a>Infraestructura de VPN
En este artículo se da por supuesto que tiene una infraestructura VPN de trabajo con Microsoft Windows Server 2016 en su lugar y ese servidor VPN de hello no está actualmente configurado tooforward de conexión solicitudes tooa RADIUS del servidor. Hola VPN infraestructura toouse un servidor RADIUS central que va a configurar en esta guía.

Si no tiene una infraestructura de trabajo en su lugar, puede crear rápidamente esta infraestructura por la siguiente directriz de hello proporcionado en numerosos tutoriales del programa de instalación VPN que puede encontrar en hello Microsoft y los sitios de terceros. 

### <a name="network-policy-and-access-services-nps-role"></a>Directiva de red y rol de servicios de acceso (NPS)

Hola servicio de rol NPS proporciona funcionalidad de cliente y servidor RADIUS de Hola. En este artículo se da por supuesto que ha instalado rol NPS de hello en un servidor miembro o controlador de dominio en su entorno. En esta guía configurará RADIUS para una configuración de VPN. Instalar el rol NPS de hello en un servidor _otros_ que el servidor VPN.

Para obtener información acerca de cómo instalar el rol NPS hello, servicio de Windows Server 2012 o posterior, consulte [instalar un servidor de directivas de mantenimiento de NAP](https://technet.microsoft.com/library/dd296890.aspx). La directiva de acceso a redes (NAP) está en desuso en Windows Server 2016. Para obtener una descripción de las prácticas recomendadas para NPS, incluidas Hola recomendación tooinstall NPS en un controlador de dominio, consulte [recomendaciones para NPS](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Licencias

Es necesaria una licencia para Azure MFA, que está disponible a través de una suscripción de Azure AD Premium, de Enterprise Mobility + Security (EMS) o de MFA. Para obtener más información, consulte [cómo tooget la autenticación multifactor Azure](multi-factor-authentication-versions-plans.md). Para realizar pruebas, puede usar una suscripción de evaluación.

### <a name="software"></a>Software

Hola extensión NPS requiere Windows Server 2008 R2 SP1 o posterior con el servicio de rol NPS Hola instalado. Todos los pasos de hello en esta guía se han ejecutado con Windows Server 2016.

### <a name="libraries"></a>Bibliotecas

Hola siguiendo dos bibliotecas es necesario:

* [Paquetes redistribuibles de Visual C++ para Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* _Módulo Microsoft Azure Active Directory para Windows PowerShell versión1.1.166.0_ o posterior. Para la versión más reciente de hello e instrucciones de instalación, consulte [Microsoft Azure Active Directory PowerShell módulo versión historial de versiones](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Estas bibliotecas no se empaquetan con hello NPS extensión archivos de instalación (versión 0.9.1.2), a pesar de la documentación existente que se indique lo contrario. Como mínimo, debe instalar los paquetes redistribuibles de hello Visual C++ para Visual Studio 2013. Hola Microsoft Azure módulo Active Directory para Windows PowerShell se instala, si todavía no está presente, a través de un script de configuración que se ejecuta como parte del proceso de instalación de Hola. No hay ninguna necesidad de tooinstall este módulo antelación si aún no está instalado.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory sincronizado con Active Directory local 

Hola toouse extensión NPS, local de usuarios deben estar sincronizados con Azure Active Directory y habilitados para la autenticación multifactor. En esta guía se da por supuesto que los usuarios locales están sincronizados con Azure Active Directory mediante AD Connect. A continuación, se proporcionan instrucciones para habilitar a los usuarios para usar MFA.
Para obtener información sobre Azure AD Connect, consulte [Integración de los directorios locales con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>Identificador de GUID de Azure Active Directory 
tooinstall Hola NPS, deberá tooknow Hola GUID de hello Azure Active Directory. Se proporcionan instrucciones para buscar Hola GUID de hello Azure Active Directory en la siguiente sección de Hola.

## <a name="configure-radius-for-vpn-connections"></a>Configuración de RADIUS para conexiones VPN

Si ha instalado el rol de servidor NPS de hello en un servidor miembro, es necesario tooconfigure tooauthenticate y autorizar el cliente VPN que solicite conexiones VPN. 

Esta sección se supone que ha instalado el rol de servidor de directivas de red de hello pero no lo ha configurado para su uso en su infraestructura.

>[!NOTE]
>Si ya tiene un servidor VPN en funcionamiento que usa un servidor RADIUS centralizado para la autenticación, puede omitir esta sección.
>

### <a name="register-server-in-active-directory"></a>Registro del servidor en Active Directory
toofunction correctamente en este escenario, el servidor NPS de hello debe toobe registrado en Active Directory.

1. Abra el Administrador del servidor.
2. En el Administrador del servidor, haga clic en **Herramientas** y, a continuación, haga clic en **Servidor de directivas de redes**. 
3. En la consola de servidor de directivas de red de hello, haga clic en **NPS (Local)**y, a continuación, haga clic en **Registrar servidor en Active Directory**. Haga clic en **Aceptar** dos veces.

 ![Servidor de directivas de redes](./media/nps-extension-vpn/image2.png)

4. Deje abierta para el procedimiento siguiente Hola Hola consola.

### <a name="use-wizard-tooconfigure-radius-server"></a>Usar el servidor RADIUS de asistente tooconfigure
Puede usar un estándar (basada en Asistente) o el servidor RADIUS de configuración avanzada opción tooconfigure Hola. En esta sección se supone el uso de Hola de opción de configuración estándar con el Asistente de Hola.

1. En la consola de servidor de directivas de red de hello, haga clic en **NPS (Local)**.
2. En la configuración estándar, seleccione **Servidor RADIUS para conexiones telefónicas o VPN** y, a continuación, haga clic en **Configurar VPN o acceso telefónico**.

 ![Configuración de VPN](./media/nps-extension-vpn/image3.png)

3. En la página Seleccione de acceso telefónico o tipo de conexiones de red privada Virtual de hello, seleccione **las conexiones de red privada Virtual**y haga clic en **siguiente**.

 ![Red privada virtual](./media/nps-extension-vpn/image4.png)

4. En la página de servidor VPN o telefónico especifique hello, haga clic en **agregar**.
5. Hola **cliente RADIUS nuevo** cuadro de diálogo, proporcione un nombre descriptivo, escriba Hola puede resolver nombre o dirección IP del servidor VPN de hello y escriba una contraseña secreta compartida. Elija una contraseña secreta compartida larga y compleja. Registre esta contraseña, según sea necesario para los pasos de la sección siguiente Hola.

 ![Nuevo cliente RADIUS](./media/nps-extension-vpn/image5.png)

6. Haga clic en **Aceptar** y, a continuación, en **Siguiente**.
7. En hello **configurar métodos de autenticación** , acepte la selección predeterminada de hello (autenticación cifrada de Microsoft versión 2 (MS-CHAPv2) o elija otra opción y haga clic en **siguiente**.

  >[!NOTE]
  >Si configura el Protocolo de autenticación extensible (EAP), debe usar MS CHAPv2 o PEAP. No se admite ningún otro tipo de EAP.
 
8. En la página especificar grupos de usuarios de hello, haga clic en **agregar** y seleccione un grupo apropiado, si existe alguno. Lo contrario, deje la selección de hello toogrant en blanco acceso tooall los usuarios.

 ![Especificar grupos de usuarios](./media/nps-extension-vpn/image7.png)

9. Haga clic en **Siguiente**.
10. En la página Especificar filtros IP de hello, haga clic en **siguiente**.
11. En la página Especificar la configuración de cifrado de hello, acepte la configuración predeterminada de Hola y haga clic en **siguiente**.

 ![Especificar cifrado](./media/nps-extension-vpn/image8.png)

12. En especificar un nombre de dominio Kerberos de hello, deje el nombre de hello en blanco, acepte la configuración predeterminada de Hola y haga clic en **siguiente**.

 ![Especificar un nombre de dominio Kerberos](./media/nps-extension-vpn/image9.png)

13. En hello telefónico completar nueva página de clientes RADIUS y de conexiones de red privada Virtual, haga clic en **finalizar**.

 ![Conexiones finalizadas](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>Comprobación de la configuración de RADIUS
En esta sección se detalla configuración Hola que había creada con el Asistente de Hola.

1. En el servidor NPS de hello, en la consola NPS (Local) de hello, expanda los clientes RADIUS y seleccione **clientes RADIUS**.
2. En el panel de detalles de hello, haga clic en el cliente RADIUS de hello creada con el asistente y haga clic en **propiedades**. propiedades de Hello para el cliente RADIUS (servidor VPN de hello) deben ser similar toothose que se muestra a continuación.

 ![Propiedades de VPN](./media/nps-extension-vpn/image11.png)

3. Haga clic en **Cancelar**.
4. En el servidor NPS de hello, en la consola NPS (Local) de hello, expanda **directivas**y seleccione **directivas de solicitud de conexión**. Debería ver directiva de conexiones VPN de Hola que es similar a la imagen de hello siguiente.

 ![Solicitudes de conexión](./media/nps-extension-vpn/image12.png)

5. En Directivas, seleccione **Directivas de red**. Debe una directiva de conexiones de red privada Virtual (VPN) que es similar a la imagen de hello siguiente.

 ![Propiedades de red](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>Configurar la autenticación de servidor VPN toouse RADIUS
En esta sección, configura la autenticación de RADIUS de hello VPN server toouse. En esta sección se da por supuesto que tiene una configuración de servidor VPN, pero no se ha configurado la autenticación de RADIUS de hello VPN server toouse. Después de configurar el servidor VPN de hello, confirme que la configuración funciona según lo previsto.

>[!NOTE]
>Si ya tiene una configuración de servidor VPN en funcionamiento que usa autenticación RADIUS, puede omitir esta sección.
>

### <a name="configure-authentication-provider"></a>Configuración del proveedor de autenticación
1. En el servidor VPN de hello, abra Administrador del servidor.
2. En el Administrador del servidor, haga clic en **Herramientas** y, a continuación, en **Enrutamiento y acceso remoto**.
3. En la consola de enrutamiento y acceso remoto de hello, haga clic en  **\[nombre del servidor\] (local)**y, a continuación, haga clic en **propiedades**.

 ![Enrutamiento y acceso remoto](./media/nps-extension-vpn/image14.png)
 
4. Hola **[propiedades de nombre del servidor} (local)** diálogo cuadro, haga clic en hello **seguridad** ficha. 
5. En hello **seguridad** , haga clic en el proveedor de autenticación, en **autenticación RADIUS**y, a continuación, **configurar**.

 ![Autenticación RADIUS](./media/nps-extension-vpn/image15.png)
 
6. En el cuadro de diálogo de autenticación RADIUS de hello, haga clic en **agregar**.
7. En Hola Agregar servidor RADIUS, en nombre del servidor, agregue Hola nombre u Hola dirección IP del servidor RADIUS de Hola que configuró en la sección anterior de Hola.
8. En el secreto compartido, haga clic en **cambio** y agregue Hola comparten contraseña secreta que ha creado y registrado anteriormente.
9. En tiempo de espera (segundos), cambie el valor de tooa de valor de hello entre **30** y **60**. Esto es necesario tooallow suficiente tiempo toocomplete Hola segundo factor de autenticación.
 
 ![Agregar servidor RADIUS](./media/nps-extension-vpn/image16.png)
 
10. Haga clic en **Aceptar** hasta cerrar todos los cuadros de diálogo.

### <a name="test-vpn-connectivity"></a>Probar la conectividad VPN
En esta sección, confirme que el cliente VPN hello es autenticado y autorizado por servidor RADIUS de hello cuando intente puerto virtual de tooconnect tooVPN. En esta sección se supone que usa Windows 10 como cliente de VPN. 

>[!NOTE]
>Si ya ha configurado un servidor VPN cliente tooconnect toohello VPN y ha guardado la configuración de hello, puede omitir Hola pasos relacionados tooconfiguring y guardar un objeto de conexión VPN.
>

1. En el equipo del cliente VPN, haga clic en **Inicio** y, a continuación, en **Configuración** (icono de engranaje).
2. En configuración de Windows, haga clic en **Red e Internet**.
3. Haga clic en **VPN**.
4. Haga clic en **Agregar una conexión VPN**.
5. En Agregar una conexión VPN, especifique Windows (integrada) como Hola proveedor de VPN y, a continuación, completa Hola restante, según corresponda y haga clic en **guardar**. 

 ![Agregar una conexión VPN](./media/nps-extension-vpn/image17.png)
 
6. Abra hello **centro de redes y recursos compartidos** en el Panel de Control.
7. Haga clic en **Cambiar configuración del adaptador**.

 ![Cambiar configuración del adaptador](./media/nps-extension-vpn/image18.png)

8. Haga clic en conexión de red VPN de Hola y haga clic en Propiedades. 

 ![Propiedades de red VPN](./media/nps-extension-vpn/image19.png)

9. En el cuadro de diálogo de propiedades VPN de hello, haga clic en hello **seguridad** ficha. 
10. En la pestaña de seguridad de hello, asegúrese de que solo **Microsoft CHAP versión 2 (MS-CHAP v2)** está seleccionada y haga clic en Aceptar.

 ![Protocolos permitidos](./media/nps-extension-vpn/image20.png)

11. Haga clic en conexión de VPN de Hola y haga clic en **conectar**.
12. En la página de configuración de hello, haga clic en **conectar**.

Una conexión correcta aparece en el registro de seguridad de hello en el servidor RADIUS de hello como 6272 de Id. de evento, como se muestra a continuación.

 ![Propiedades de evento](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Guía de solución de problemas
Se supone que la configuración de VPN funcionase correctamente antes de configurar Hola VPN server toouse un servidor RADIUS centralizado para la autenticación y autorización. En este caso, es probable que el problema de hello puede deberse a una configuración incorrecta de hello servidor RADIUS o hello uso de un nombre de usuario no válido o la contraseña. Por ejemplo, si usas sufijo UPN alternativo de hello en nombre de usuario de hello, intento de inicio de sesión de Hola podría fallar (debe usar Hola el mismo nombre de cuenta para obtener los mejores resultados). 

tootroubleshoot estos problemas, un toostart lugar ideal es registros de eventos de seguridad de tooexamine hello en Hola servidor RADIUS. búsqueda de tiempo de toosave para los eventos, puede usar Hola basada en roles servidor de acceso y directivas de redes vista personalizada en el Visor de eventos, como se muestra a continuación. Id. de evento 6273 indica donde hello servidor de directivas de red denegado usuario tooa de acceso de eventos. 

 ![Visor de eventos](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Configuración de Multi-Factor Authentication
Esta sección proporciona instrucciones para habilitar a los usuarios para MFA y para configurar las cuentas para la verificación en dos pasos. 

### <a name="enable-multi-factor-authentication"></a>Habilitar Multi-Factor Authentication
En esta sección, se habilitan cuentas de Azure AD para MFA. Hola de uso **portal clásico** tooenable a los usuarios para MFA. 

1. Abra un explorador y navegue demasiado[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Inicie sesión como administrador de Hola.
3. En el portal de hello, en panel de navegación izquierdo hello, haga clic en **ACTIVE DIRECTORY**.

 ![Directorio predeterminado](./media/nps-extension-vpn/image23.png)

4. En la columna de nombre de hello, haga clic en **directorio predeterminado** (o en otro directorio, si procede).
5. En la página de inicio rápido de hello, haga clic en **configurar**.

 ![Configurar valor predeterminado](./media/nps-extension-vpn/image24.png)

6. En la página de configuración de hello, desplácese hacia abajo y, en la sección de la autenticación multifactor de hello, haga clic en **administrar la configuración del servicio**.

 ![Administrar la configuración de MFA](./media/nps-extension-vpn/image25.png)
 
7. En la página de la autenticación multifactor de hello, revise la configuración predeterminada del servicio de hello y, a continuación, haga clic en **usuarios**. 

 ![Usuarios de MFA](./media/nps-extension-vpn/image26.png)
 
8. En la página de usuarios de hello, seleccione los usuarios de Hola que desea tooenable para MFA y, a continuación, haga clic en **habilitar**.

 ![Propiedades](./media/nps-extension-vpn/image27.png)
 
9. Cuando se le solicite, haga clic en **Habilitar autenticación multifactor**.

 ![Habilitar MFA](./media/nps-extension-vpn/image28.png)
 
10. Haga clic en **Cerrar**. 
11. Actualice la página de Hola. Hola estado de autenticación Multifactor es tooEnabled modificada.

Para obtener información acerca de cómo los usuarios de tooenable para la autenticación multifactor, consulte [Introducción a la autenticación multifactor Azure en la nube de hello](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>Configuración de cuentas para la verificación en dos pasos
Una vez que una cuenta se ha habilitado para MFA, los usuarios no son toosign capaz de tooresources regulado por la directiva de MFA de hello hasta que ha configurado correctamente una toouse de dispositivo de confianza para el segundo factor de autenticación Hola haber utilizado la verificación en dos pasos.

En esta sección, configurará un dispositivo de confianza para su uso con la verificación en dos pasos. Hay varias opciones disponibles para tooconfigure estos elementos, incluidos Hola siguientes:

* **Aplicación móvil**. Instalar la aplicación de Microsoft Authenticator hello en un dispositivo Windows Phone, Android o iOS. Según las directivas de su organización, es necesario toouse Hola aplicación en uno de dos modos: recibir notificaciones para comprobaciones (una notificación se inserta tooyour dispositivo) o usar código de comprobación (es necesario tooenter una comprobación de código que actualiza cada 30 segundos). 
* **Llamada de teléfono móvil o mensaje de texto**. Puede recibir un mensaje de texto o una llamada de teléfono automática. Con la opción de llamada de teléfono de hello, responder a la llamada de hello y presione tooauthenticate de inicio de sesión de # Hola. Con la opción de texto hello, puede responder a mensajes de texto de toohello o escriba el código de comprobación de hello en interfaz de inicio de sesión de Hola.
* **Llamada de teléfono de la oficina**. Este proceso es Hola igual a la se ha descrito para las llamadas de teléfono automatizadas anteriores.

Siga estas instrucciones para configurar una notificación de inserción de dispositivo toouse Hola aplicación móvil tooreceive para la comprobación.

1. Inicie sesión demasiado[https://aka.ms/mfasetup](https://aka.ms/mfasetup) o a cualquier sitio, como [https://portal.azure.com](https://portal.azure.com), donde se requiere tooauthenticate con sus credenciales basadas en MFA. 
2. Al iniciar sesión con su nombre de usuario y la contraseña, se le presentará una pantalla que solicita tooset cuenta de hello para la comprobación de seguridad adicional.

 ![Seguridad adicional](./media/nps-extension-vpn/image29.png)

3. Haga clic en **Configurar ahora**.
4. En la página de comprobación de seguridad adicionales de hello, seleccione un tipo de contacto (aplicación móvil, teléfono del trabajo o teléfono de autenticación). A continuación, seleccione un país o región y seleccione un método. método Hello varía según el tipo de contacto que seleccione. Por ejemplo, si elige la aplicación móvil, puede seleccionar si las notificaciones de tooreceive de comprobación o toouse un código de comprobación. Hola que siga da por sentado que elija **aplicación móvil** como hello, póngase en contacto con tipo.

 ![Teléfono de autenticación](./media/nps-extension-vpn/image30.png)

5. Seleccione Aplicación móvil, haga clic en **Recibir notificaciones de comprobación** y, a continuación, haga clic en **Configurar**. 

 ![Comprobación con aplicación móvil](./media/nps-extension-vpn/image31.png)
 
6. Si aún no lo ha hecho lo ha hecho, instale aplicación móvil de autenticador de hello en el dispositivo. 
7. Siga las instrucciones de Hola Hola aplicación móvil tooscan Hola presentada el código de barras o escribir información de hello manualmente y, a continuación, haga clic en **realiza**.

 ![Configuración de la aplicación móvil](./media/nps-extension-vpn/image32.png)

8. En la página de comprobación de seguridad adicionales de hello, haga clic en **contacto me** y respuesta toonotification enviado tooyour dispositivo.
9. En la página de comprobación de seguridad adicionales de hello, escriba un número de contacto en caso de que pierda la aplicación móvil de acceso toohello y haga clic en **siguiente**.

 ![Número de teléfono móvil](./media/nps-extension-vpn/image33.png)
 
10. En hello comprobación de seguridad adicional, haga clic en **realiza**.

Hola dispositivo ya está configurado tooprovide un segundo método de comprobación. Para obtener información sobre cómo configurar cuentas para la verificación en dos pasos, consulte [Configurar mi cuenta para la verificación en dos pasos](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Instalación y configuración de la extensión NPS

Esta sección proporciona instrucciones para configurar VPN toouse Azure MFA para la autenticación de cliente con hello servidor VPN.

Después de instalar y configurar la extensión NPS hello, toda la autenticación de cliente basada en RADIUS que es procesado por este servidor es necesario toouse MFA de Azure. Si no todos los usuarios VPN se inscriben en Azure MFA, puede configurar otro RADIUS server tooauthenticate a los usuarios que no sean toouse configurado MFA. O bien, puede crear una entrada del registro que permite a los usuarios sus tooprovide un segundo factor de autenticación, solo si están inscritos en MFA. 

Crear un nuevo valor de cadena denominado _REQUIRE_USER_MATCH en HKLM\SOFTWARE\Microsoft\AzureMfa_y establezca Hola valor tooTRUE o FALSE. 

 ![Require User Match (Requerir coincidencia de usuario)](./media/nps-extension-vpn/image34.png)
 
Si el valor de hello es conjunto tooTRUE o no establecida, todas las solicitudes de autenticación están sujetas desafío tooan MFA. Si el valor de Hola se establece tooFALSE, desafíos MFA se emiten sólo toousers que están inscritos en MFA. Usar solo hello valor FALSE en las pruebas o en entornos de producción durante un período de incorporación.

### <a name="acquire-azure-active-directory-guid-id"></a>Obtener el identificador de GUID de Azure Active Directory

Como parte de configuración de Hola de hello extensión NPS, necesita credenciales de administrador de toosupply y Hola identificador Azure Active Directory para el inquilino de Azure AD. Hola pasos siguientes muestran cómo identificador de inquilino de hello tooget.

1. Inicie sesión en toohello portal de Azure en [https://portal.azure.com](https://portal.azure.com) como administrador global de Hola de hello Azure de inquilinos.
2. Hola barra de navegación izquierda, haga clic en hello **Azure Active Directory** icono.
3. Haga clic en **Propiedades**.
4. toocopy el Portapapeles de toohello de Id. de directorio, seleccione hello **copia** icono.
 
 ![Identificador de directorio](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Instalar extensión NPS Hola
Hola extensión NPS debe toobe instalado en un servidor que tiene la directiva de red de Hola y rol de servicios de acceso (NPS) instalado y que funcione como servidor RADIUS de hello en el diseño. No instale la extensión NPS de hello en el servidor de escritorio remoto.

1. La extensión NPS Hola de descargar [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Copie el servidor NPS toohello de hello el programa de instalación (NpsExtnForAzureMfaInstaller.exe) del archivo ejecutable.
3. En el servidor NPS de hello, haga doble clic en **NpsExtnForAzureMfaInstaller.exe**. Cuando se le solicite, haga clic en **Ejecutar**.
4. En hello extensión de NPS para el cuadro de diálogo de MFA de Azure, revisar los términos de licencia del software de hello, comprobar **acepto los términos de licencia de toohello y condiciones**y haga clic en **instalar**.

 ![Extensión NPS](./media/nps-extension-vpn/image36.png)
 
5. Hola extensión de NPS para el cuadro de diálogo de MFA de Azure, haga clic en **cerrar**.  

 ![Instalación correcta](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurar certificados para su uso con la extensión NPS hello mediante un script de PowerShell
comunicaciones seguras tooensure y seguridad, deberá tooconfigure certificados para su uso por extensión NPS Hola. los componentes NPS Hola incluyen un script de Windows PowerShell que configure un certificado autofirmado para su uso con NPS. 

script de Hola realiza Hola siguientes acciones:

* Crea un certificado autofirmado
* Asocia la clave pública del certificado tooservice principal en Azure AD
* Hola a almacenes de certificados en el almacén del equipo local de Hola
* Concede acceso toohello clave privada del certificado toohello usuario de red
* Reinicia el servicio Servidor de directivas de redes

Si desea toouse sus propios certificados, necesita tooassociate Hola público de la entidad de seguridad de servicio de certificado toohello en Azure AD y así sucesivamente.
script de Hola toouse, proporcionar extensión Hola con sus credenciales administrativas de Azure Active Directory y Hola Id. de inquilino de Azure Active Directory que copió anteriormente. Ejecutar script de Hola en cada servidor NPS donde se instala la extensión NPS Hola.

1. Abra un símbolo del sistema administrativo de Windows PowerShell.
2. En el símbolo del sistema de PowerShell hello, escriba _cd 'c:\Program Files\Microsoft\AzureMfa\Config'_y presione **ENTRAR**.
3. Escriba _.\AzureMfsNpsExtnConfigSetup.ps1_ y presione **ENTRAR**. 
 * script de Hola comprueba toosee si está instalado el módulo de PowerShell de Azure Active Directory de Hola. Si no está instalado, el script de Hola instala módulo Hola.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Después de que el script de Hola comprueba la instalación de Hola Hola del módulo de PowerShell, muestra el cuadro de diálogo de módulo de Azure Active Directory PowerShell Hola. En el cuadro de diálogo de hello, escriba sus credenciales de administrador de Azure AD y la contraseña y haga clic en **iniciar sesión en**. 
 
 ![Inicio de sesión de PowerShell](./media/nps-extension-vpn/image39.png)
 
5. Cuando se le solicite, pegue el Id. de inquilino de Hola que copió anteriormente toohello Portapapeles y presione **ENTRAR**. 

 ![Id. de inquilino](./media/nps-extension-vpn/image40.png)

6. script de Hola crea un certificado autofirmado y realiza otros cambios de configuración. salida de Hello es similar a la imagen de Hola se muestra a continuación.

 ![Certificado autofirmado](./media/nps-extension-vpn/image41.png)

7. Reinicie el servidor de Hola.
 
### <a name="verify-configuration"></a>Comprobación de la configuración
configuración de hello tooverify, deberá tooestablish una nueva conexión de VPN con el servidor VPN. Cuando se especifica correctamente las credenciales para la autenticación principal, Hola conexión VPN espera Hola autenticación secundaria toosucceed antes de establecer conexión hello, tal y como se muestra a continuación. 

 ![Comprobación de la configuración](./media/nps-extension-vpn/image42.png)

Si se autentica correctamente con el método de verificación secundaria hello que configuró previamente en Azure MFA, son recursos toohello conectado. Sin embargo, si la autenticación secundaria hello no es correcta, se le deniega el acceso tooresource. 

En el ejemplo de Hola siguiente, Hola autenticador aplicación en un dispositivo Windows phone es autenticación secundaria de hello tooprovide usado.

 ![Comprobar cuenta](./media/nps-extension-vpn/image43.png)

Una vez que se haya autenticado correctamente utilizando el método secundario hello, se le concede acceso toohello puerto virtual en el servidor VPN de Hola. Sin embargo, puesto que han toouse requiere un método de autenticación secundario con una aplicación móvil en un dispositivo de confianza, registro de hello en proceso es más seguro que sería utilizar solo un nombre de usuario / contraseña.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Ver los registros del Visor de eventos para eventos de inicio de sesión correcto
eventos de inicio de sesión correcto de tooview hello en los registros del Visor de eventos de Windows hello, puede emitir Hola siguiendo el registro de seguridad de Windows de Windows PowerShell comando tooquery hello en el servidor NPS de Hola.

eventos de inicio de sesión correcto de tooquery en registros de Visor de eventos de seguridad de hello, usar hello siguiente comando,
* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 

 ![Visor de eventos de seguridad](./media/nps-extension-vpn/image44.png)
 
También puede ver el registro de seguridad de Hola u Hola servicios de acceso y directivas de redes vista personalizada, tal y como se muestra a continuación:

 ![Acceso a la directiva de red](./media/nps-extension-vpn/image45.png)

En el servidor de Hola donde instaló la extensión NPS de Hola para MFA de Azure, puede encontrar registros del Visor de eventos de aplicación toohello específico de extensión en **aplicaciones y servicios Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL

 ![Número de eventos](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Guía de solución de problemas
Si la configuración de hello no funciona según lo esperado, un tootroubleshoot de toostart lo ideal es tooverify que Hola usuario toouse configurado Azure MFA. Tener usuario Hola conectarse demasiado[https://portal.azure.com](https://portal.azure.com). Si a los usuarios se les solicita la autenticación secundaria y se pueden autenticar correctamente, puede descartar una configuración incorrecta de Azure MFA.

Si funciona Azure MFA para usuarios de hello, debe revisar los registros de eventos relevantes Hola. Esto incluye registros de eventos de seguridad, operativa de la puerta de enlace y de Azure MFA de Hola que se describen en la sección anterior de Hola. 

A continuación, se muestra un ejemplo de salida del registro de seguridad que muestra un evento de inicio de sesión incorrecto (identificador de evento 6273):

 ![Registro de seguridad](./media/nps-extension-vpn/image47.png)

A continuación se muestra un evento relacionado de hello AzureMFA registros:

 ![Registros de Azure MFA](./media/nps-extension-vpn/image48.png)

tooperform avanzada solucionar problemas de opciones, consulte archivos de registro de la formato de hello NPS base de datos donde está instalado el servicio NPS Hola. Estos archivos de registro se crean en la carpeta _%SystemRoot%\System32\Logs_ como archivos de texto delimitado por comas. Para obtener una descripción de estos archivos de registro, consulte [Interpretación de los archivos de registro de formato de la base de datos de NPS](https://technet.microsoft.com/library/cc771748.aspx). 

las entradas de Hello en estos archivos de registro son difíciles de toointerpret sin importarlos en una hoja de cálculo o una base de datos. Puede encontrar un número de IAS analizadores en línea tooassist en interpretar Hola archivos de registro. A continuación se muestra la salida de hello de uno estos descargable [aplicación shareware](http://www.deepsoftware.com/iasviewer): 

 ![Aplicación shareware](./media/nps-extension-vpn/image49.png)

Por último, para más opciones de solución de problemas, puede utilizar un analizador de protocolos, como Wireshark o el [Analizador de mensajes de Microsoft](https://technet.microsoft.com/library/jj649776.aspx). Hello siguiente imagen desde Wireshark muestra mensajes de Hola RADIUS entre servidor VPN de Hola y Hola NPS.

 ![Analizador de mensajes de Microsoft](./media/nps-extension-vpn/image50.png)

Para más información, consulte [Integración de la infraestructura NPS existente con Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Pasos siguientes
[¿Cómo tooget la autenticación multifactor Azure](multi-factor-authentication-versions-plans.md)

[Puerta de enlace de Escritorio remoto y Servidor Azure Multi-Factor Authentication con RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integración de los directorios locales con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

