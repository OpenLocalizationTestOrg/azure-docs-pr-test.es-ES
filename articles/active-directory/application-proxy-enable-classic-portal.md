---
title: "Proxy de aplicación de Azure AD en el portal clásico de hello aaaEnable | Documentos de Microsoft"
description: "Activar Proxy de aplicación de portal de Azure clásico de Hola e instalar Hola conectores de proxy inverso de Hola."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Habilitar a Proxy de aplicación de portal clásico de Hola y descargar conectores
Este artículo le guiará a través de hello pasos tooenable Proxy de aplicación de Microsoft Azure AD para el directorio de nube en Azure AD.

Si no está familiarizado con lo que el Proxy de aplicación puede ayudarle a hacerlo, obtenga más información sobre [cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Requisitos previos del proxy de la aplicación
Antes de poder habilitar y usar servicios de Proxy de aplicación, debe toohave:

* Una [suscripción Basic o Premium a Microsoft Azure AD](active-directory-editions.md) y un directorio de Azure AD del que sea administrador global.
* Servidor que ejecuta Windows Server 2012 R2 o 2016, en el que puede instalar Hola conector del Proxy de aplicación. servidor Hello envía solicitudes de servicios de Proxy de aplicación de toohello en la nube de Hola y necesita una aplicación de toohello de conexión de HTTP o HTTPS que va a publicar.
  * Para que tooyour de inicio de sesión único publicado aplicaciones, esta máquina debe estar-unidos al dominio en el dominio de hello misma instancia de AD como aplicaciones de Hola que va a publicar. Para obtener información, consulte [Inicio de sesión único con el proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)
* Si su organización usa proxy de lectura de internet, servidores tooconnect toohello [trabajo existente servidores proxy local](application-proxy-working-with-proxy-servers.md) para obtener más información acerca de cómo tooconfigure ellos.

## <a name="open-your-ports"></a>Apertura de los puertos

tooprepare su entorno para el Proxy de aplicación de Azure AD, primero debe tooenable comunicación tooAzure los centros de datos. Si hay un firewall en la ruta de acceso de hello, asegúrese de que está abierto, por lo que Hola que conector podrá efectuar HTTPS (TCP) solicita toohello Proxy de aplicación.

1. Siguiente Hola abrir puertos demasiado**saliente** tráfico:

   | Número de puerto | Cómo se usa |
   | --- | --- |
   | 80 | Descarga de revocación de certificados (CRL) enumera al validar el certificado SSL de Hola |
   | 443 | Toda la comunicación saliente con hello servicio Proxy de aplicación |

   Si el firewall fuerza el tráfico según los usuarios toooriginating, abra estos puertos para el tráfico procedente de servicios de Windows que se ejecutan como un servicio de red.

   > [!IMPORTANT]
   > tabla de Hello refleja los requisitos de puerto de Hola para versiones de conector 1.5.132.0 y versiones más recientes. Si todavía tiene una versión anterior del conector, también necesita hello tooenable siguientes puertos: 5671, 8080, 9090, 9091, 9350, 9352 y 10100 – 10120.
   >
   >Para obtener información acerca de cómo actualizar la versión más reciente de toohello de conectores, consulte [conectores de Proxy de aplicación de AD de Azure comprender](application-proxy-understand-connectors.md#automatic-updates).

2. Si el firewall o proxy permite crear listas blancas con DNS, puede servicebus.windows.net y toomsappproxy.net de conexiones de lista blanca de direcciones. Si no es así, necesita tooallow acceso toohello [intervalos de direcciones IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653), que se actualizan cada semana.

3. Hola de uso [herramienta de prueba de Azure AD aplicación Proxy conector puertos](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que el conector puede comunicarse con servicio de Proxy de aplicación Hola. Como mínimo, asegúrese de que región de EE. UU. Central de Hola y Hola región más cercana tooyou tienen todas las marcas de verificación verde. Además, cuantas más marcas de verificación verde haya, mayor resistencia habrá.

## <a name="enable-application-proxy-in-azure-ad"></a>Habilitación del proxy de la aplicación en Azure AD
1. Inicie sesión como administrador en hello [portal de Azure clásico](https://manage.windowsazure.com/).
2. Vaya tooActive directorio y seleccione el directorio de hello en el que desee tooenable Proxy de aplicación.

    ![Active Directory (icono)](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Seleccione **configurar** desde la página directory hello y desplácese hacia abajo demasiado**Proxy de aplicación**.
4. Alternar **habilitar a los servicios de Proxy de aplicación para este directorio** demasiado**habilitado**.

    ![Habilitación del proxy de la aplicación](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Seleccione **Descargar ahora**. Hola **Azure AD Proxy conector de descarga de la aplicación** se abre. Lea y acepte los términos de licencia de Hola y haga clic en **descargar** toosave archivo Windows Installer (.exe) hello para el conector de Hola.

## <a name="install-and-register-hello-connector"></a>Instalar y registrar Hola conector
1. Ejecutar **AADApplicationProxyConnectorInstaller.exe** en servidor hello preparado correspondiente toohello requisitos previos.
2. Siga las instrucciones de hello en hello Asistente tooinstall.
3. Durante la instalación, son tooregister solicitadas Hola conector con hello Proxy de aplicación del inquilino de Azure AD.

   * Proporcione sus credenciales de administrador global de Azure AD. Su inquilino de administrador global puede ser diferente de sus credenciales de Microsoft Azure.
   * Asegúrese de que el servicio Proxy de aplicación Hola a Hola, administrador que registra Hola conector está en Hola mismo directorio donde haya habilitado. Por ejemplo, si el dominio del inquilino de hello es contoso.com, Hola, administrador debe ser admin@contoso.com o cualquier otro alias de ese dominio.
   * Si **configuración de seguridad mejorada de Internet Explorer** se establece demasiado**en** en el servidor de hello, pantalla de bienvenida registro podría bloquearse. acceso de tooallow, siga las instrucciones de hello en el mensaje de error de saludo. Asegúrese de que Internet Explorer Enhanced Security está desactivado.
   * Si el registro del conector no funciona, consulte [Solucionar problemas de Proxy de aplicación](active-directory-application-proxy-troubleshoot.md).  
4. Cuando se completa la instalación de hello, dos servicios nuevos se agregan tooyour server:

   * **Conector de Proxy de aplicación de Microsoft AAD** habilita la conectividad

     * **Actualizador del conector del proxy de aplicación de Microsoft AAD** es un servicio de actualización automática. Periódicamente busca nuevas versiones del conector de Hola y conector Hola se actualiza según sea necesario.

     ![Servicios de conector del proxy de la aplicación (captura de pantalla)](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Haga clic en **finalizar** en la ventana de instalación de hello.

Para más información sobre los conectores, consulte [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md) (Descripción de los conectores del proxy de aplicación de Azure AD).

Si desea tener alta disponibilidad, debe implementar al menos dos conectores. toodeploy más conectores, repita los pasos 2 y 3. Cada conector debe estar registrado de manera independiente.

Si desea toouninstall Hola conector, debe desinstalar los servicios del conector de Hola y Hola actualizador. Reinicie el servicio de equipo toofully remove Hola.

## <a name="next-steps"></a>Pasos siguientes
Ya estás listo demasiado[publicar aplicaciones con Proxy de aplicación](active-directory-application-proxy-publish.md).

Si tiene aplicaciones que se encuentran en redes independientes o en distintas ubicaciones, puede utilizar conectores distintos de conector grupos tooorganize hello en unidades lógicas. Obtenga más información sobre cómo [trabajar con conectores de Proxy de aplicación](active-directory-application-proxy-connectors.md).
