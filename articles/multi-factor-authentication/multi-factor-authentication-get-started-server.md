---
title: "aaaGetting inicia el servidor de autenticación multifactor de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe la forma en que tooget se inicia con el servidor Azure MFA."
services: multi-factor-authentication
keywords: "servidor de autenticación, página de activación de la aplicación de azure multi factor autenticación, descarga del servidor de autenticación"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Introducción a Hola servidor Azure Multi-factor Authentication

<center>![MFA local](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Ahora que hemos determinado toouse servidor Multi-factor Authentication local, vamos a empezar. Esta página cubre una nueva instalación del servidor de Hola y configurarla con local de Active Directory. Si ya tiene instalado hello MFA server y está buscando tooupgrade, consulte [actualizar toohello servidor más reciente de Azure Multi-factor Authentication](multi-factor-authentication-server-upgrade.md). Si desea obtener información acerca de cómo instalar solo el servicio de web hello, consulte [implementación Hola servicio Web de aplicación móvil de Azure Multi-factor Authentication Server](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Planeamiento de la implementación

Antes de descargar Hola servidor Azure Multi-factor Authentication, piense en ¿cuáles son sus requisitos de alta disponibilidad y carga. Utilice esta información toodecide cómo y dónde toodeploy.

Una buena directriz para cantidad Hola de memoria necesaria es número Hola de usuarios que espera tooauthenticate de forma regular.

| Usuarios | RAM |
| ----- | --- |
| 1-10,000 | 4 GB |
| 10,001-50,000 | 8 GB |
| 50,001-100,000 | 12 GB |
| 100,000-200,001 | 16 GB |
| 200,001+ | 32 GB |

¿Necesita tooset varios servidores para alta disponibilidad o equilibrio de carga? Hay una serie de formas tooset esta configuración con el servidor Azure MFA. Cuando se instala el primer servidor de MFA de Azure, se convierte en maestra Hola. Todos los servidores adicionales se convierten en subordinado y sincronizan automáticamente los usuarios y la configuración con el maestro de Hola. A continuación, puede configurar un servidor principal y se rest Hola actúan como copia de seguridad, o se puede configurar Equilibrio de carga entre todos los servidores de Hola.

Cuando se desconecta un maestro servidor Azure MFA, los servidores subordinados Hola todavía pueden procesar las solicitudes de comprobación de dos pasos. Sin embargo, no puede agregar nuevos usuarios y a los usuarios existentes no se pueden actualizar su configuración hasta que se vuelve a estar conectado master de Hola o subordinado se promociona.

### <a name="prepare-your-environment"></a>Preparación del entorno

Asegúrese de que servidor de Hola que esté usando para la autenticación multifactor Azure cumple Hola según los requisitos:

| Requisitos del Servidor Azure Multi-Factor Authentication | Description |
|:--- |:--- |
| Hardware |<li>200 MB de espacio de disco duro</li><li>Procesador compatible con x32 o x64</li><li>1 GB o más de RAM</li> |
| Software |<li>Windows Server 2008 o superior si el host de hello es un sistema operativo de servidor</li><li>Windows 7 o posterior si el host de hello es un sistema operativo cliente</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 o posterior si instalar Hola usuario web o portal SDK del servicio</li> |

### <a name="azure-mfa-server-components"></a>Componentes del servidor Azure MFA

Hay tres componentes web que componen el servidor Azure MFA:

* Servicio SDK - habilita la comunicación con Hola otros componentes y se instala en el servidor de aplicaciones de Azure MFA hello Web
* Portal de usuarios: un sitio web IIS que permite a los usuarios tooenroll en Azure la autenticación multifactor (MFA) y mantener sus cuentas.
* Servicio Web de la aplicación móvil: permite el uso de una aplicación móvil como aplicación de Microsoft Authenticator hello para la verificación en dos pasos.

Los tres componentes pueden instalarse en hello mismo servidor si el servidor de hello está orientado a internet. Si importantes componentes hello, Hola SDK del servicio Web está instalado en el servidor de aplicaciones de Azure MFA de Hola y Hola Portal de usuarios y servicio de la aplicación Web móvil se instalan en un servidor con conexión a internet.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Requisitos de firewall del Servidor Azure Multi-Factor Authentication

Cada servidor MFA debe ser capaz de toocommunicate en toohello de salida de puerto 443 siguientes direcciones:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Si están restringidos firewalls salientes en el puerto 443, abra Hola después de intervalos de direcciones IP:

| Subred IP | Máscara de red | Rango de direcciones IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Si no está usando la característica de confirmación de evento de Hola y los usuarios no están usando tooverify de aplicaciones móviles desde dispositivos de red corporativa de hello, solo necesita Hola siguientes intervalos:

| Subred IP | Máscara de red | Rango de direcciones IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Descargar Hola servidor Azure Multi-factor Authentication

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Hola izquierda, seleccione **Active Directory**
3. Haga clic en **Usuarios y grupos**.
4. Haga clic en **Todos los usuarios**.
5. Haga clic en **Multi-Factor Authentication**.
6. En la sección **Multi-Factor Authentication**, seleccione **configuración del servicio**.

   ![Página de configuración del servicio](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. En la página de configuración de servicios de hello, en la parte inferior de Hola de pantalla de bienvenida, haga clic en **Go toohello portal**. Se abrirá una nueva página.
7. Haga clic en **Descargas**.
8. Haga clic en hello **descargar** vincular y guardar el instalador de Hola.

   ![Descargar servidor MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Mantenga esta página abierta ya nos referiremos tooit después de la ejecución instalador Hola.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Instalar y configurar Hola servidor Azure Multi-factor Authentication

Ahora que ha descargado servidor hello puede instalar y configurar. Asegúrese de que ese servidor hello en que va a instalar cumple con los requisitos mencionados en hello planeamiento de sección.

1. Haga doble clic en el ejecutable hello.
2. En la pantalla de bienvenida Seleccionar carpeta de instalación, asegúrese de que esa carpeta hello es correcta y haga clic en **siguiente**.
3. Una vez completada la instalación de hello, haga clic en **finalizar**.  se inicia el Asistente para configuración de Hola.
4. En la pantalla de bienvenida de hello configuración asistente, compruebe **Skip mediante Hola Asistente para configuración de autenticación** y haga clic en **siguiente**.  cierra el Asistente de Hola y Hola server se inicia.

   ![Nube](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Nuevo en la página de Hola que descargamos servidor hello desde, haga clic en hello **generar credenciales de activación** botón. Copiar esta información en el servidor Azure MFA en los cuadros de Hola Hola proporcionado y haga clic en **activar**.

## <a name="send-users-an-email"></a>Enviar un correo electrónico a los usuarios

implementación de tooease, permitir que el servidor MFA toocommunicate con los usuarios. Servidor MFA puede enviar un correo electrónico tooinform ellas que se hayan inscrito para verificación en dos pasos.

correo electrónico de Hello que envía debe determinar cómo configurar los usuarios para la verificación en dos pasos. Por ejemplo, si es capaz de tooimport números de teléfono desde el directorio de la empresa de hello, correo electrónico de hello debe incluir números de teléfono de hello predeterminada para que los usuarios sepan qué tooexpect. Si no se importan los números de teléfono o los usuarios van a aplicación móvil de toouse hello, enviarles un correo electrónico que les dirija toocomplete inscripción de su cuenta. Incluir un Portal de usuarios de Azure Multi-factor Authentication de hipervínculo toohello en correo electrónico de Hola.

contenido de Hola de correo electrónico de hello también varía según método hello de comprobación que se ha establecido para el usuario de hello (llamada de teléfono, SMS o aplicación móvil).  Por ejemplo, si el usuario de hello toouse requiere un PIN para la autenticación, correo electrónico de hello diciendo su PIN inicial que se estableció en.  Los usuarios es necesaria toochange su PIN durante su primera comprobación.

### <a name="configure-email-and-email-templates"></a>Configuración del correo electrónico y las plantillas de correo electrónico

Haga clic en el icono de correo electrónico de hello en hello izquierdo tooset la configuración de Hola para enviar estos correos electrónicos. Esta página es donde puede escribir información de hello SMTP de tu correo electrónico de servidor y el envío de correo electrónico mediante la comprobación de hello **enviar correos electrónicos toousers** casilla de verificación.

![Configuración del correo electrónico del servidor MFA](./media/multi-factor-authentication-get-started-server/email1.png)

En la pestaña contenido de correo electrónico de hello, puede ver plantillas de correo electrónico de Hola que están disponible toochoose desde. Dependiendo de cómo haya configurado la verificación de los usuarios tooperform en dos pasos, elija la plantilla de Hola que mejor se adapte a.

![Plantillas de correo electrónico del servidor MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importación de usuarios desde Active Directory

Ahora que el servidor hello instalado deberá tooadd a los usuarios. Puede elegir toocreate manualmente, importar usuarios desde Active Directory, o configurar la sincronización automática con Active Directory.

### <a name="manual-import-from-active-directory"></a>Importación manual desde Active Directory

1. Hola servidor Azure MFA, Hola izquierda, seleccione **usuarios**.
2. En la parte inferior de hello, seleccione **importar desde Active Directory**.
3. Ahora puede ya sea buscar usuarios individuales o búsqueda hello directorio de AD para las unidades organizativas con usuarios en ellos.  En este caso, especificamos usuarios Hola OU.
4. Resalte todos los usuarios Hola Hola derecho y haga clic en **importación**.  Debe aparecer una ventana emergente que le indica que la operación se realizó correctamente.  Ventana de importación de hello cerrar.

   ![Importación de usuarios del servidor MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Sincronización automática con Active Directory

1. Hola servidor Azure MFA, Hola izquierda, seleccione **integración de directorios**.
2. Navegue toohello **sincronización** ficha.
3. En la parte inferior de hello, elija **agregar**
4. Hola **Agregar elemento de sincronización** cuadro que aparece elija Hola dominio, unidad organizativa **o** grupo de seguridad, la configuración, valores predeterminados de método y los valores predeterminados de idioma de esta sincronización de tareas y haga clic en **Agregar**.
5. Hola casilla **habilitar la sincronización con Active Directory** y elija un **intervalo de sincronización** entre un minuto y 24 horas.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Modo Hola servidor Azure Multi-factor Authentication controla los datos de usuario

Cuando usas Hola la autenticación multifactor (MFA) Server local, los datos de un usuario se almacenan en servidores locales de Hola. Ningún dato de usuario persistentes se almacena en la nube de Hola. Cuando el usuario Hola lleva a cabo una verificación en dos pasos, Hola servidor MFA envía datos toohello comprobación de Hola de tooperform del servicio de nube de Azure MFA. Cuando estas solicitudes de autenticación se envían toohello servicio en la nube, hello campos siguientes se envían en la solicitud de Hola y de registros para que estén disponibles en los informes de uso y autenticación del cliente de Hola. Algunos de los campos de hello son opcionales, por lo que puede habilitar o deshabilitar en hello servidor Multi-factor Authentication. comunicación de Hola de hello servicio de nube de servidor MFA toohello MFA usa SSL/TLS en el puerto 443 de salida. Estos campos son:

* Id. exclusivo: nombre de usuario o Id. interno de Servidor MFA
* Nombre y apellidos (opcional)
* Dirección de correo electrónico (opcional)
* Número de teléfono: al realizar una llamada de voz o autenticación por SMS
* Token de dispositivo: al realizar la autenticación de una aplicación móvil
* Modo de autenticación
* Resultado de autenticación
* Nombre de Servidor MFA
* IP de Servidor MFA
* IP de cliente: si está disponible

Además toohello campos anteriores, resultado (éxito o denegación) de la verificación de Hola y el motivo de las denegaciones también es almacenan con los datos de autenticación de Hola y están disponibles a través de informes de uso y autenticación de Hola.

## <a name="back-up-and-restore-azure-mfa-server"></a>Copia de seguridad y restauración del servidor Azure MFA

Asegurarse de que tiene una buena copia de seguridad es un tootake paso importante con cualquier sistema.

tooback servidor de MFA de Azure, asegúrese de que tiene una copia del programa Hola a **C:\Program programa\multi-Factor Authentication Server\Data** carpeta incluido hello **PhoneFactor.pfdata** archivo. 

En caso de una restauración es necesario Hola completa pasos siguientes:

1. Vuelva a instalar el servidor Azure MFA en un servidor nuevo.
2. Activar Hola de nuevo servidor de MFA de Azure.
3. Hola Stop **MultiFactorAuth** servicio.
4. Sobrescribir hello **PhoneFactor.pfdata** con hello copia la copia de seguridad.
5. Iniciar hello **MultiFactorAuth** servicio.

nuevo servidor de Hello es ahora a trabajar con datos de copia de seguridad originales usuario y configuración de Hola.

## <a name="next-steps"></a>Pasos siguientes

- Instalar y configurar hello [Portal de usuarios](multi-factor-authentication-get-started-portal.md) de autoservicio del usuario.
- Instalar y configurar Hola servidor Azure MFA con [servicio de federación de Active Directory](multi-factor-authentication-get-started-adfs.md), [autenticación RADIUS](multi-factor-authentication-get-started-server-radius.md), o [autenticación LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instalación y configuración de [Puerta de enlace de Escritorio remoto y Servidor Azure Multi-Factor Authentication con RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Implementar el servicio Web de aplicación móvil de Azure Multi-factor Authentication Server hello](multi-factor-authentication-get-started-server-webservice.md).
- [Escenarios avanzados con Azure Multi-Factor Authentication y VPN de terceros](multi-factor-authentication-advanced-vpn-configurations.md).
