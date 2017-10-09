---
title: "integración de la puerta de enlace de escritorio con la extensión de Azure MFA NPS aaaRemote | Documentos de Microsoft"
description: "Este artículo describe la integración de la infraestructura de la puerta de enlace de escritorio remoto con Azure MFA con la extensión de servidor de directivas de redes (NPS) de Hola para Microsoft Azure."
services: active-directory
keywords: "Azure MFA, integración de puerta de enlace de Escritorio remoto, Azure Active Directory, extensión Servidor de directivas de redes"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Integrar la infraestructura de la puerta de enlace de escritorio remoto mediante la extensión de servidor de directivas de redes (NPS) de Hola y Azure AD

Este artículo proporciona detalles para integrar la infraestructura de la puerta de enlace de escritorio remoto con Azure Multi-factor Authentication (MFA) con la extensión de servidor de directivas de redes (NPS) de Hola para Microsoft Azure. 

Hola extensión de servicio de directivas de redes (NPS) de Azure permite el uso de Azure de la autenticación del cliente de servicio de autenticación remota telefónica de usuario (RADIUS) de los clientes toosafeguard's basado en la nube [la autenticación multifactor (MFA)](multi-factor-authentication.md). Esta solución proporciona una comprobación de dos pasos para agregar una segunda capa de inicios de sesión de seguridad toouser y las transacciones.

Este artículo proporciona instrucciones paso a paso para integrar la infraestructura de hello NPS con Azure MFA mediante la extensión NPS Hola de Azure. Esto permite la comprobación de seguridad para los usuarios que intentan toolog en tooa puerta de enlace de escritorio remoto. 

Hola directivas de redes y servicios de acceso (NPS) ofrece a las empresas Hola capacidad toodo Hola a continuación:
* Definir ubicaciones centrales para la administración de Hola y control de las solicitudes de red al especificar quién puede conectarse, Hola a qué horas del día en que se permiten las conexiones, duración de las conexiones y el nivel de Hola de seguridad que los clientes deben usar tooconnect y así sucesivamente. En vez de especificar estas directivas en cada VPN o servidor de puerta de enlace de Escritorio remoto (RD), estas directivas se especifican una vez en una ubicación central. Hola protocolo RADIUS proporciona Hola centralizada de autenticación, autorización y contabilidad (AAA). 
* Establecer y aplicar directivas de mantenimiento de cliente de protección de acceso a redes (NAP) que determinan si los dispositivos se conceden acceso restringido o sin restricción toonetwork recursos.
* Proporcione un medio tooenforce autenticación y autorización para conmutadores Ethernet y puntos de acceso inalámbricos compatibles con too802.1x de acceso.    

Normalmente, las organizaciones usar toosimplify NPS (RADIUS) y centralizar la administración de Hola de VPN directivas. Sin embargo, muchas organizaciones también usar NPS toosimplify y centralizar la administración de Hola de directivas de autorización de conexión de escritorio de escritorio remoto (CAP de RD). 

Las organizaciones también pueden integrar NPS con seguridad de Azure MFA tooenhance y proporcionar un alto nivel de compatibilidad. Esto ayuda a asegurarse de que los usuarios establezcan toolog de comprobación de dos pasos en toohello puerta de enlace de escritorio remoto. Para los usuarios toobe concedido acceso, deberán proporcionar su combinación de nombre de usuario/contraseña con la información que Hola usuario tiene en su control. Esta información debe ser de confianza y no duplicable fácilmente, como un número de teléfono móvil, el número fijo o una aplicación en un dispositivo móvil, entre otros.

Disponibilidad de toohello anteriores de hello extensión NPS para Azure, los clientes que deseaban tooimplement verificacion de integran NPS y los entornos de Azure MFA tenían tooconfigure y mantienen un servidor independiente de MFA en el entorno local de hello como documentados en [puerta de enlace de escritorio remoto y servidor de Azure Multi-factor Authentication con RADIUS](multi-factor-authentication-get-started-server-rdg.md).

disponibilidad de Hola de extensión NPS de Hola para Azure le proporciona las organizaciones Hola elección toodeploy una solución MFA basándose en local o una autenticación de cliente RADIUS de basado en la nube MFA solución toosecure.

## <a name="authentication-flow"></a>Flujo de autenticación

Para que los usuarios toobe concede acceso a los recursos de toonetwork a través de una puerta de enlace de escritorio remoto, deben cumplir con las condiciones de hello especificadas en una directiva de autorización de conexión de escritorio remoto (CAP de RD) y una directiva de autorización de recursos de escritorio remoto (RAP de RD). CAP de RD especificar quién está autorizado tooconnect tooRD puertas de enlace. RAP de RD especificar recursos de red de hello, como equipos de escritorio remotos o aplicaciones remotas, se permite que el usuario hello tooconnect toothrough Hola puerta de enlace de escritorio remoto. 

Una puerta de enlace de escritorio remoto puede ser toouse configurado un almacén de directivas central de CAP de RD. RAP de RD no puede usar una directiva central, tal y como se procesan en hello puerta de enlace de escritorio remoto. Un ejemplo de una puerta de enlace de escritorio remoto configurado toouse un almacén de directivas central de CAP de RD es un servidor NPS tooanother de cliente RADIUS que sirve como almacén de directiva central Hola.

Cuando Hola extensión NPS para Azure está integrado con hello NPS y puerta de enlace de escritorio remoto, flujo de una autenticación correcta de hello es como sigue:

1. servidor de puerta de enlace de escritorio remoto de Hello recibe una solicitud de autenticación de un recurso de tooa tooconnect de usuario de escritorio remoto, como una sesión de escritorio remoto. Actúa como cliente RADIUS, servidor de puerta de enlace de escritorio remoto de hello convierte el mensaje de solicitud de acceso RADIUS de hello solicitud tooa y envía Hola de mensajes toohello RADIUS (NPS) del servidor donde se instala la extensión NPS Hola. 
2. Hola nombre de usuario y se comprueba la combinación de contraseña en Active Directory y Hola usuario está autenticado.
3. Si todos los Hola condiciones como se especifica en Hola de solicitud de conexión de NPS y se cumplen las directivas de redes de hello (por ejemplo, la hora del día o de grupo restricciones de pertenencia), Hola extensión NPS desencadena una solicitud de autenticación secundaria con Azure MFA. 
4. MFA de Azure se comunica con Azure AD, recupera los detalles de usuario de Hola y realiza la autenticación secundaria de hello mediante método hello configurado por el usuario de hello (mensaje de texto, aplicación móvil etc.). 
5. Cuando se realiza correctamente de hello desafío MFA, MFA de Azure se comunica extensión de hello resultado toohello NPS.
6. servidor NPS Hola donde se instala la extensión de Hola envía un mensaje de aceptación de acceso RADIUS para el servidor de puerta de enlace de escritorio remoto de toohello de directivas de hello CAP de RD.
7. se concede acceso usuario Hello toohello solicita el recurso de red a través de hello puerta de enlace de escritorio remoto.

## <a name="prerequisites"></a>Requisitos previos
En esta sección se detalla los requisitos previos de hello necesarios antes de integrar Azure MFA con hello puerta de enlace de escritorio remoto. Antes de comenzar, debe tener Hola siguiendo los requisitos previos en su lugar.  

* Infraestructura de Servicios de Escritorio remoto (RDS)
* Licencia de Azure MFA
* Software de Windows Server
* Directiva de red y rol de servicios de acceso (NPS)
* Azure AD sincronizado con AD local 
* Identificador de GUID de Azure Active Directory

### <a name="remote-desktop-services-rds-infrastructure"></a>Infraestructura de Servicios de Escritorio remoto (RDS)
Debe tener una infraestructura de Servicios de Escritorio remoto (RDS) en funcionamiento. Si no lo hace, a continuación, puede crear rápidamente esta infraestructura de Azure con hello siguientes de inicio rápido plantilla: [implementación Crear colección de sesiones de escritorio remoto](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

Si desea toomanually crear una infraestructura RDS local rápidamente para realizar pruebas, seguimiento Hola pasos toodeploy uno. 
**Para más información**: [Implementación de RDS con la plantilla de inicio rápido de Azure](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) e [Implementación de la infraestructura de RDS básica](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). 

### <a name="licenses"></a>Licencias
Es necesaria una licencia para Azure MFA, que está disponible a través de una suscripción de Azure AD Premium, de Enterprise Mobility + Security (EMS) o de MFA. Para obtener más información, consulte [cómo tooget la autenticación multifactor Azure](multi-factor-authentication-versions-plans.md). Para realizar pruebas, puede usar una suscripción de evaluación.

### <a name="software"></a>Software
Hola extensión NPS requiere Windows Server 2008 R2 SP1 o posterior con el servicio de rol NPS Hola instalado. Todos los pasos de hello en esta sección se han ejecutado con Windows Server 2016.

### <a name="network-policy-and-access-services-nps-role"></a>Directiva de red y rol de servicios de acceso (NPS)
Hola servicio de rol NPS proporciona cliente y servidor RADIUS de hello funcionalidad, así como el servicio de mantenimiento de directiva de acceso de red. Este rol debe instalarse en al menos dos equipos de la infraestructura: Hola puerta de enlace de escritorio remoto y otro servidor miembro o controlador de dominio. De forma predeterminada, rol Hola ya está presente en el equipo de hello configurado como puerta de enlace de escritorio remoto de Hola.  También debe instalar rol NPS de hello en al menos en otro equipo, como un servidor miembro o controlador de dominio.

Para obtener información acerca de cómo instalar el rol NPS Hola servicio Windows Server 2012 o anterior, vea [instalar un servidor de directivas de mantenimiento de NAP](https://technet.microsoft.com/library/dd296890.aspx). Para obtener una descripción de las prácticas recomendadas para NPS, incluidas Hola recomendación tooinstall NPS en un controlador de dominio, consulte [recomendaciones para NPS](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory sincronizado con Active Directory local 
Hola toouse extensión NPS, local de los usuarios deben estar sincronizados con Azure AD y habilitados para MFA. En esta sección se da por supuesto que los usuarios locales están sincronizados con Azure AD mediante AD Connect. Para obtener información sobre Azure AD Connect, consulte [Integración de los directorios locales con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>Identificador de GUID de Azure Active Directory
tooinstall NPS, debe tooknow Hola GUID de hello Azure AD. A continuación se proporcionan instrucciones para buscar Hola GUID de hello Azure AD.

## <a name="configure-multi-factor-authentication"></a>Configuración de Multi-Factor Authentication 
Esta sección proporciona instrucciones para la integración de Azure MFA con hello puerta de enlace de escritorio remoto. Como administrador, debe configurar el servicio de Azure MFA Hola antes de que los usuarios pueden registrarse ellos mismos sus aplicaciones o dispositivos de varios factores.

Siga los pasos de hello en [Introducción a la autenticación multifactor Azure en la nube de hello](multi-factor-authentication-get-started-cloud.md) tooenable MFA para los usuarios de Azure AD. 

### <a name="configure-accounts-for-two-step-verification"></a>Configuración de cuentas para la verificación en dos pasos
Una vez que una cuenta se ha habilitado para MFA, no se puede iniciar sesión en tooresources rige por hello directiva de MFA hasta que se ha configurado correctamente un dispositivo de confianza toouse de segundo factor de autenticación Hola han autenticado mediante verificación en dos pasos.

Siga los pasos de hello en [¿qué significa la autenticación multifactor Azure para mí?](./end-user/multi-factor-authentication-end-user.md) toounderstand y configurar correctamente los dispositivos para MFA con su cuenta de usuario.

## <a name="install-and-configure-nps-extension"></a>Instalación y configuración de la extensión NPS
Esta sección proporciona instrucciones para configurar RDS infraestructura toouse Azure MFA para la autenticación de cliente con hello puerta de enlace de escritorio remoto.

### <a name="acquire-azure-active-directory-guid-id"></a>Obtener el identificador de GUID de Azure Active Directory

Como parte de configuración de Hola de hello extensión NPS, necesita credenciales de administrador de toosupply y el identificador de Azure AD de hello para el inquilino de Azure AD. Hola siguientes pasos muestra cómo identificador de inquilino de hello tooget.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador global de Hola de hello Azure de inquilinos.
2. Hola barra de navegación izquierda, seleccione hello **Azure Active Directory** icono.
3. Seleccione **Propiedades**.
4. En la hoja de propiedades de hello, al lado de hello Id. de directorio, haga clic en hello **copia** icono, tal y como se muestra a continuación, toocopy Hola identificador tooclipboard.

 ![Propiedades](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Instalar extensión NPS Hola
Instalar extensión NPS de hello en un servidor que tenga instalado el rol de servicios de acceso (NPS) y de saludo directiva de red. Esto funciona como servidor RADIUS de hello para el diseño. 

>[!Important]
> Asegúrese de que no instalar extensión NPS de hello en el servidor de puerta de enlace de escritorio remoto.
> 

1. Descargar hello [extensión NPS](https://aka.ms/npsmfa). 
2. Copie el servidor NPS toohello de hello el programa de instalación (NpsExtnForAzureMfaInstaller.exe) del archivo ejecutable.
3. En el servidor NPS de hello, haga doble clic en **NpsExtnForAzureMfaInstaller.exe**. Cuando se le solicite, haga clic en **Ejecutar**.
4. En hello extensión de NPS para el cuadro de diálogo de MFA de Azure, revisar los términos de licencia del software de hello, comprobar **acepto los términos de licencia de toohello y condiciones**y haga clic en **instalar**.
 
  ![Instalación de Azure MFA](./media/nps-extension-remote-desktop-gateway/image2.png)

5. Hola extensión de NPS para el cuadro de diálogo de MFA de Azure, haga clic en Cerrar. 

  ![Extensión NPS para Azure MFA](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurar certificados para su uso con la extensión NPS hello mediante un script de PowerShell
A continuación, se necesitan certificados de tooconfigure para su uso por hello NPS extensión tooensure las comunicaciones seguras y la seguridad. los componentes NPS Hola incluyen un script de Windows PowerShell que configure un certificado autofirmado para su uso con NPS. 

script de Hola realiza Hola siguientes acciones:

* Crea un certificado autofirmado
* Asocia la clave pública del certificado tooservice principal en Azure AD
* Hola a almacenes de certificados en el almacén del equipo local de Hola
* Concede acceso de usuario de la red toohello clave privada del certificado de toohello
* Reinicia el servicio Servidor de directivas de redes

Si desea toouse sus propios certificados, necesita tooassociate Hola público de la entidad de seguridad de servicio de certificado toohello en Azure AD y así sucesivamente.

script de Hola toouse, proporcionar extensión Hola con sus credenciales de administrador de AD de Azure y Hola Id. de inquilino de Azure AD que copió anteriormente. Ejecutar script de Hola en cada servidor NPS donde instaló la extensión NPS Hola. A continuación, Hola siguientes:

1. Abra un símbolo del sistema administrativo de Windows PowerShell.
2. En el símbolo del sistema de PowerShell hello, escriba **cd 'c:\Program Files\Microsoft\AzureMfa\Config'**y presione **ENTRAR**.
3. Escriba _.\AzureMfsNpsExtnConfigSetup.ps1_ y presione **ENTRAR**. script de Hola comprueba toosee si está instalado el módulo de PowerShell de Azure Active Directory de Hola. Si no está instalado, el script de Hola instala módulo Hola.

  ![PowerShell de Azure AD](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Después de que el script de Hola comprueba la instalación de Hola Hola del módulo de PowerShell, muestra el cuadro de diálogo de módulo de Azure Active Directory PowerShell Hola. En el cuadro de diálogo de hello, escriba sus credenciales de administrador de Azure AD y la contraseña y haga clic en **inicio de sesión**.

  ![Abrir cuenta de Powershell](./media/nps-extension-remote-desktop-gateway/image5.png)

5. Cuando se le solicite, pegue el Id. de inquilino de Hola que copió anteriormente toohello Portapapeles y presione **ENTRAR**.

  ![Escriba el identificador del inquilino](./media/nps-extension-remote-desktop-gateway/image6.png)

6. script de Hola crea un certificado autofirmado y realiza otros cambios de configuración. Hola resultado debe ser similar a la imagen de Hola se muestra a continuación.

  ![Certificado autofirmado](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>Configuración de los componentes de NPS en la puerta de enlace de Escritorio remoto
En esta sección, configurar directivas de autorización de conexión de puerta de enlace de escritorio remoto de Hola y otras opciones de RADIUS.

flujo de autenticación de Hello requiere que los mensajes RADIUS intercambiarse entre Hola hello y puerta de enlace de escritorio remoto servidor NPS donde está instalado el servidor NPS Hola. Esto significa que debe configurar la configuración del cliente RADIUS en la puerta de enlace de escritorio remoto y Hola servidor NPS donde se instala la extensión NPS Hola. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Configurar el almacén central del toouse de directivas de autorización de conexiones para la puerta de enlace de escritorio remoto
Directivas de autorización de conexión a Escritorio remoto (CAP de RD) especifican los requisitos de hello para el servidor de puerta de enlace de escritorio remoto de conexión tooa. Las CAP de RD pueden almacenarse localmente (valor predeterminado) o pueden almacenarse en un almacén de CAP de RD central que ejecute NPS. integración de tooconfigure de MFA de Azure con RDS, es necesario utilizar de Hola de toospecify de un almacén central.

1. En el servidor de puerta de enlace de escritorio remoto de hello, abra **el administrador del servidor**. 
2. En el menú de hello, haga clic en **herramientas**, seleccione demasiado**servicios de escritorio remoto**y, a continuación, haga clic en **el Administrador de puerta de enlace de escritorio remoto**.

  ![Servicios de Escritorio remoto](./media/nps-extension-remote-desktop-gateway/image8.png)

3. Hola Administrador de puerta de enlace de escritorio remoto, haga clic en  **\[nombre del servidor\] (Local)**y haga clic en **propiedades**.

  ![Nombre del servidor](./media/nps-extension-remote-desktop-gateway/image9.png)

4. En el cuadro de diálogo de propiedades de hello, seleccione hello **CAP de RD** pestaña almacén.
5. En la ficha de almacén de CAP de RD de hello, seleccione **servidor Central que ejecuta NPS**. 
6. Hola **escriba un nombre o dirección IP de servidor hello que ejecuta NPS** campo, tipo hello IP dirección o el nombre del servidor de Hola donde instaló la extensión NPS Hola.

  ![Escriba el nombre o dirección IP](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. Haga clic en **Agregar**.
8. Hola **secreto compartido** cuadro de diálogo, escriba un secreto compartido y, a continuación, haga clic en **Aceptar**. Asegúrese de registrar este secreto compartido y almacenar de forma segura el registro de hello.

 >[!NOTE]
 >Se usa el secreto compartido tooestablish confianza entre clientes y servidores RADIUS de Hola. Cree una contraseña larga y compleja.
 >

 ![Secreto compartido](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Haga clic en **Aceptar** cuadro de diálogo de tooclose Hola.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>Configuración del valor de tiempo de espera de RADIUS en el NPS de la puerta de enlace de Escritorio remoto
tooensure hay es hora de credenciales de los usuarios toovalidate, realizar la verificación en dos pasos, recibir respuestas y responde mensajes tooRADIUS, es el valor de tiempo de espera RADIUS de hello tooadjust necesarios.

1. En el servidor de puerta de enlace de escritorio remoto de hello, en el administrador del servidor, haga clic en **herramientas**y, a continuación, haga clic en **servidor de directivas de red**. 
2. Hola **NPS (Local)** de la consola, expanda **clientes y servidores RADIUS**y seleccione **servidor RADIUS remoto**.

 ![Servidor RADIUS remoto](./media/nps-extension-remote-desktop-gateway/image12.png)

3. En el panel de detalles de hello, haga doble clic en **grupo de servidores de puerta de enlace de TS**.

 >[!NOTE]
 >Este grupo de servidores RADIUS se creó al configurar Hola server central para las directivas NPS. Hola puerta de enlace de escritorio remoto reenvía el servidor de toothis de mensajes RADIUS o un grupo de servidores, si más de un grupo de Hola.
 >

4. Hola **propiedades de grupo de servidores de puerta de enlace de TS** cuadro de diálogo, dirección IP de hello select o nombre de servidor NPS configurado CAP de RD toostore de Hola y, a continuación, haga clic en **editar**. 

 ![Grupo de servidores de puerta de enlace de TS](./media/nps-extension-remote-desktop-gateway/image13.png)

5. Hola **Editar servidor RADIUS** cuadro de diálogo, seleccione hello **equilibrio de carga** ficha.
6. Hola **equilibrio de carga** ficha Hola **quita el número de segundos sin respuesta antes de solicitud se considera** campo, cambiar el valor predeterminado de Hola de 3 valor tooa entre 30 y 60 segundos.
7. Hola **número de segundos entre solicitudes cuando el servidor se identifica como no disponible** campo, cambie el valor predeterminado de hello del valor de tooa de 30 segundos que es mayor que el valor de Hola que especificó en el paso anterior de Hola de tooor igual.

 ![Editar servidor Radius](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Haga clic en Aceptar dos veces tooclose Hola los cuadros de diálogo.

### <a name="verify-connection-request-policies"></a>Verificación de las directivas de solicitud de conexión 
De forma predeterminada, al configurar la puerta de enlace de escritorio remoto de hello toouse un almacén de directivas central para las directivas de autorización de conexión, Hola puerta de enlace de escritorio remoto es el servidor NPS toohello de tooforward configurado CAP solicitudes. servidor NPS Hola con la extensión de Azure MFA Hola instalado, solicitud de acceso RADIUS de Hola de procesos. Hola pasos muestra cómo Directiva de solicitud de conexión predeterminada de tooverify Hola. 

1. En hello puerta de enlace de escritorio remoto, en la consola NPS (Local) de hello, expanda **directivas**y seleccione **directivas de solicitud de conexión**.
2. Haga clic con el botón derecho en **Directivas de solicitud de conexión** y haga doble clic en **Directiva de autorización de puerta de enlace de TS**.
3. Hola **propiedades de la directiva de autorización de puerta de enlace de TS** diálogo cuadro, haga clic en hello **configuración** ficha.
4. En la pestaña **Configuración**, bajo Reenvío de solicitud de conexión, haga clic en **Autenticación**. Cliente RADIUS está configurado tooforward solicitudes de autenticación.

 ![Configuración de autenticación](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Haga clic en **Cancelar**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Configure NPS en el servidor de Hola donde está instalado Hola extensión NPS
servidor NPS Hola donde extensión NPS de hello es necesidades instalado toobe tooexchange capaz de RADIUS mensajes con servidor NPS de hello en hello puerta de enlace de escritorio remoto. Este mensaje de tooenable exchange, necesitará tooconfigure Hola NPS componentes en servidor hello donde está instalado el servicio de extensión NPS Hola. 

### <a name="register-server-in-active-directory"></a>Registro del servidor en Active Directory
toofunction correctamente en este escenario, el servidor NPS de hello debe toobe registrado en Active Directory.

1. Abra el **Administrador del servidor**.
2. En el Administrador del servidor, haga clic en **Herramientas** y, a continuación, haga clic en **Servidor de directivas de redes**. 
3. En la consola de servidor de directivas de red de hello, haga clic en **NPS (Local)**y, a continuación, haga clic en **Registrar servidor en Active Directory**. 
4. Haga clic en **Aceptar** dos veces.

 ![Registro del servidor en AD](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Deje abierta para el procedimiento siguiente Hola Hola consola.

### <a name="create-and-configure-radius-client"></a>Creación y configuración del cliente RADIUS 
Hola puerta de enlace de escritorio remoto debe toobe configurado como un servidor NPS de toohello de cliente RADIUS. 

1. En servidor NPS Hola Hola extensión NPS está instalado, en hello **NPS (Local)** de la consola, haga clic en **clientes RADIUS** y haga clic en **nuevo**.

 ![Nuevo cliente RADIUS](./media/nps-extension-remote-desktop-gateway/image17.png)

2. Hola **cliente RADIUS nuevo** diálogo cuadro, proporcione un nombre descriptivo, como _puerta de enlace_, y Hola dirección IP o nombre DNS del servidor de puerta de enlace de escritorio remoto de Hola. 
3. Hola **secreto compartido** hello y **Confirmar secreto compartido** campos, escriba Hola mismo secreto que usó anteriormente.

 ![Nombre y dirección](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Haga clic en **Aceptar** el cuadro de diálogo de tooclose Hola RADIUS nuevo cliente.

### <a name="configure-network-policy"></a>Configuración de la directiva de red
Servidor de recuperación Hola NPS con hello extensión de Azure MFA es Hola directiva central designado almacén Hola directiva de autorización de conexiones (CAP). Por lo tanto, deberá tooimplement un límite en las solicitudes de conexiones válidas de hello NPS server tooauthorize.  

1. En la consola NPS (Local) de hello, expanda **directivas**y haga clic en **las directivas de red**.
2. Haga clic en **servidores de acceso a las conexiones tooother**y haga clic en **Duplicar directiva**. 

 ![Duplicar directiva](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Haga clic en **servidores de acceso de copia de las conexiones tooother**y haga clic en **propiedades**.

 ![Propiedades de red](./media/nps-extension-remote-desktop-gateway/image20.png)

4. Hola **servidores de acceso de copia de las conexiones tooother** cuadro de diálogo, en nombre de directiva, escriba un nombre adecuado, como **RDG_CAP**. Marque la casilla **Directiva habilitada** y seleccione **Conceder acceso**. Si lo desea, en Tipo de acceso a la red, seleccione **Puerta de enlace de Escritorio remoto** o puede dejarlo como **Sin especificar**.

 ![Copia de las conexiones](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Haga clic en hello **restricciones** ficha y compruebe **tooconnect de permitir que los clientes sin negociar un método de autenticación**.

 ![Permitir a los clientes tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. Si lo desea, haga clic en hello **condiciones** pestaña y agregar las condiciones que deben cumplirse para hello conexión toobe autorizado, por ejemplo, pertenencia a un grupo de Windows específico.

 ![Condiciones](./media/nps-extension-remote-desktop-gateway/image23.png)

7. Haga clic en **Aceptar**. Cuando tooview solicitada hello tema de ayuda correspondiente, haga clic en **No**.
8. Asegúrese de que la nueva directiva se encuentra en parte superior de Hola de lista de hello, que está habilitada la directiva de hello, y que concede acceso.

 ![Directivas de red](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Comprobación de la configuración
configuración de hello tooverify, deberá toolog en hello puerta de enlace de escritorio remoto con un cliente RDP adecuado. Toouse seguro de que sea una cuenta está permitida por las directivas de autorización de conexión y está habilitada para Azure MFA. 

Como se muestra en la imagen de Hola a continuación, puede usar hello **acceso Web a Escritorio remoto** página.

![Acceso web de Escritorio remoto](./media/nps-extension-remote-desktop-gateway/image25.png)

Cuando se especifica correctamente las credenciales para la autenticación principal, cuadro de diálogo de conexión a Escritorio remoto de hello muestra un estado de iniciar una conexión remota, tal y como se muestra a continuación. 

Si se autentica correctamente con método de autenticación secundario Hola que configuró previamente en Azure MFA, son recursos toohello conectado. Sin embargo, si la autenticación secundaria hello no es correcta, se le deniega el acceso tooresource. 

![Iniciar la conexión remota](./media/nps-extension-remote-desktop-gateway/image26.png)

En el ejemplo de Hola siguiente, Hola autenticador aplicación en un dispositivo Windows phone es autenticación secundaria de hello tooprovide usado.

![Cuentas](./media/nps-extension-remote-desktop-gateway/image27.png)

Una vez que se haya autenticado correctamente utilizando el método de autenticación secundario hello, se registran en hello puerta de enlace de escritorio remoto como normalmente. Sin embargo, dado que son toouse requiere un método de autenticación secundario con una aplicación móvil en un dispositivo de confianza, proceso de registro de hello es más seguro que sería lo contrario.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Ver los registros del Visor de eventos para eventos de inicio de sesión correcto
tooview Hola inicio de sesión de eventos correctos en los registros del Visor de eventos de Windows hello, puede emitir Hola siguientes comando tooquery hello Windows Terminal Services de Windows PowerShell y registros de seguridad de Windows.

tooquery inicio de sesión de eventos correctos de registros operativos de puerta de enlace de hello _(Visor de eventos y servicios Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, usar hello siguientes comandos:

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL 
* Este comando muestra los eventos de Windows que muestra el usuario Hola cumple los requisitos de directiva de autorización de recursos (RAP de RD) y se le concedió acceso.

![Visualización del Visor de eventos](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL
* Este comando muestra los eventos de Hola que se muestran cuando el usuario cumplió los requisitos de directiva de autorización de conexión.

![Autorización de conexión](./media/nps-extension-remote-desktop-gateway/image29.png)

También puede ver este registro y filtrar por los identificadores de los eventos, 300 y 200. eventos de inicio de sesión correcto de tooquery en registros de Visor de eventos de seguridad de hello, utilice Hola siguiente comando:

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 
* Este comando se puede ejecutar en cualquier Hola NPS central o servidor de puerta de enlace de escritorio remoto de bienvenida. 

![Eventos de inicio de sesión correcto](./media/nps-extension-remote-desktop-gateway/image30.png)

También puede ver el registro de seguridad de Hola u Hola servicios de acceso y directivas de redes vista personalizada, tal y como se muestra a continuación:

![Directiva de red y servicios de acceso](./media/nps-extension-remote-desktop-gateway/image31.png)

En el servidor de Hola donde instaló la extensión NPS de Hola para MFA de Azure, puede encontrar registros del Visor de eventos de aplicación toohello específico de extensión en _aplicaciones y servicios Logs\Microsoft\AzureMfa_. 

![Registros de aplicación del Visor de eventos](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Guía de solución de problemas

Si la configuración de hello no funciona según lo esperado, Hola primer lugar toostart tootroubleshoot es tooverify que Hola usuario toouse configurado Azure MFA. Hacer que el usuario de Hola se conecten toohello [portal de Azure](https://portal.azure.com). Si a los usuarios se les solicita la comprobación secundaria y se pueden autenticar correctamente, puede descartar una configuración incorrecta de Azure MFA.

Si funciona Azure MFA para usuarios de hello, debe revisar los registros de eventos relevantes Hola. Esto incluye registros de eventos de seguridad, operativa de la puerta de enlace y de Azure MFA de Hola que se describen en la sección anterior de Hola. 

A continuación, se muestra un ejemplo de salida del registro de seguridad que muestra un evento de inicio de sesión incorrecto (identificador de evento 6273).

![Evento de inicio de sesión incorrecto](./media/nps-extension-remote-desktop-gateway/image33.png)

A continuación se muestra un evento relacionado de hello AzureMFA registros:

![Registro de Azure MFA](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform avanzada solucionar problemas de opciones, consulte archivos de registro de la formato de hello NPS base de datos donde está instalado el servicio NPS Hola. Estos archivos de registro se crean en la carpeta _%SystemRoot%\System32\Logs_ como archivos de texto delimitado por comas. 

Para obtener una descripción de estos archivos de registro, consulte [Interpretación de los archivos de registro de formato de la base de datos de NPS](https://technet.microsoft.com/library/cc771748.aspx). las entradas de Hello en estos archivos de registro pueden ser difícil toointerpret sin importarlos en una hoja de cálculo o una base de datos. Puede encontrar varios analizadores de IAS tooassist en línea, en la interpretación de Hola archivos de registro. 

Hello imagen siguiente muestra la salida de hello de uno estos descargable [aplicación shareware](http://www.deepsoftware.com/iasviewer). 

![Aplicación shareware](./media/nps-extension-remote-desktop-gateway/image35.png)

Por último, para más opciones de solución de problemas, puede utilizar un analizador de protocolos, como el [Analizador de mensajes de Microsoft](https://technet.microsoft.com/library/jj649776.aspx). 

la imagen siguiente desde el analizador de mensajes de Microsoft Hello muestra el tráfico de red filtrado en el protocolo RADIUS que contiene el nombre de usuario de hello **Contoso\AliceC**.

![Analizador de mensajes de Microsoft](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Pasos siguientes
[¿Cómo tooget la autenticación multifactor Azure](multi-factor-authentication-versions-plans.md)

[Puerta de enlace de Escritorio remoto y Servidor Azure Multi-Factor Authentication con RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integración de los directorios locales con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
