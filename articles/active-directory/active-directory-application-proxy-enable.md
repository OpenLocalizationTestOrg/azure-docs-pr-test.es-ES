---
title: 'aaaAzure AD App Proxy: empezar a instalar el conector | Documentos de Microsoft'
description: "Activar Proxy de aplicación Hola portal de Azure e instale Hola conectores de proxy inverso de Hola."
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
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Empezar a trabajar con el Proxy de aplicación e instalar el conector de Hola
Este artículo le guiará a través de hello pasos tooenable Proxy de aplicación de Microsoft Azure AD para el directorio de nube en Azure AD.

Si no está aún pone de Proxy de aplicación tenga en cuenta las ventajas de seguridad y productividad de hello tooyour organización, obtenga más información sobre [cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Requisitos previos del proxy de la aplicación
Antes de poder habilitar y usar servicios de Proxy de aplicación, debe toohave:

* Una [suscripción Basic o Premium a Microsoft Azure AD](active-directory-editions.md) y un directorio de Azure AD del que sea administrador global.
* Servidor que ejecuta Windows Server 2012 R2 o 2016, en el que puede instalar Hola conector del Proxy de aplicación. servidor Hello necesita servicios de Proxy de aplicación de toobe tooconnect puede toohello en la nube de Hola y Hola aplicaciones que se va a publicar en local.
  * Para tooyour de inicio de sesión único las aplicaciones publicadas mediante la delegación limitada de Kerberos, esta máquina debe estar-unidos al dominio en el dominio de hello misma instancia de AD como aplicaciones de Hola que va a publicar. Para obtener información, vea la información sobre [la delegación limitada de kerberos para el inicio de sesión único con el proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md).

Si su organización usa proxy de lectura de internet, servidores tooconnect toohello [trabajo existente servidores proxy local](application-proxy-working-with-proxy-servers.md) para obtener más información acerca de cómo tooconfigure ellos antes de obtienen iniciado con el Proxy de aplicación.

## <a name="open-your-ports"></a>Apertura de los puertos

tooprepare su entorno para el Proxy de aplicación de Azure AD, primero debe tooenable comunicación tooAzure los centros de datos. Si hay un firewall en la ruta de acceso de hello, asegúrese de que está abierto, por lo que Hola que conector podrá efectuar HTTPS (TCP) solicita toohello Proxy de aplicación.

1. Siguiente Hola abrir puertos demasiado**saliente** tráfico:

   | Número de puerto | Cómo se usa |
   | --- | --- |
   | 80 | Descarga de revocación de certificados (CRL) enumera al validar el certificado SSL de Hola |
   | 443 | Toda la comunicación saliente con hello servicio Proxy de aplicación |

   Si el firewall fuerza el tráfico según los usuarios toooriginating, abra estos puertos para el tráfico de servicios de Windows que se ejecutan como un servicio de red.

   > [!IMPORTANT]
   > tabla de Hello refleja los requisitos de puerto de Hola para versiones de conector 1.5.132.0 y versiones más recientes. Si todavía tiene una versión anterior del conector, también necesita hello tooenable siguiendo los puertos en suma too80 y 443:5671, 8080, 9090-9091, 9350, 9352, 10100 – 10120.
   >
   >Para obtener información acerca de cómo actualizar la versión más reciente de toohello de conectores, consulte [conectores de Proxy de aplicación de AD de Azure comprender](application-proxy-understand-connectors.md#automatic-updates).

2. Si el firewall o proxy permite crear listas blancas con DNS, puede servicebus.windows.net y toomsappproxy.net de conexiones de lista blanca de direcciones. Si no es así, necesita tooallow acceso toohello [intervalos de direcciones IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653), que se actualizan cada semana.

3. Microsoft utiliza certificados de tooverify de cuatro direcciones. Permitir toohello acceso si no lo ha hecho para otros productos de las siguientes direcciones URL:
   * mscrl.microsoft.com:80
   * crl.microsoft.com:80
   * ocsp.msocsp.com:80
   * www.microsoft.com:80

4. El conector necesita acceso toologin.windows.net y login.microsoftonline.net para el proceso de registro de hello.

5. Hola de uso [herramienta de prueba de Azure AD aplicación Proxy conector puertos](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que el conector puede comunicarse con servicio de Proxy de aplicación Hola. Como mínimo, asegúrese de que región de EE. UU. Central de Hola y Hola región más cercana tooyou tienen todas las marcas de verificación verde. Además, cuantas más marcas de verificación verde haya, mayor resistencia habrá.

## <a name="install-and-register-a-connector"></a>Instalación y registro de un conector
1. Inicie sesión como administrador en hello [portal de Azure](https://portal.azure.com/).
2. El directorio actual aparece bajo el nombre de usuario en la esquina superior derecha de Hola. Si necesita toochange directorios, seleccione ese icono.
3. Vaya demasiado**Azure Active Directory** > **Proxy de aplicación**.

   ![Navegue tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Seleccione **Descargar conector**.

   ![Descarga del conector](./media/active-directory-application-proxy-enable/download_connector.png)

5. Ejecutar **AADApplicationProxyConnectorInstaller.exe** en servidor hello preparado correspondiente toohello requisitos previos.
6. Siga las instrucciones de hello en hello Asistente tooinstall. Durante la instalación, son tooregister solicitadas Hola conector con hello Proxy de aplicación del inquilino de Azure AD.

   * Proporcione sus credenciales de administrador global de Azure AD. Su inquilino de administrador global puede ser diferente de sus credenciales de Microsoft Azure.
   * Asegúrese de que el servicio Proxy de aplicación Hola a Hola, administrador que registra Hola conector está en Hola mismo directorio donde haya habilitado. Por ejemplo, si el dominio del inquilino de hello es contoso.com, Hola, administrador debe ser admin@contoso.com o cualquier otro alias de ese dominio.
   * Si **configuración de seguridad mejorada de Internet Explorer** se establece demasiado**en** en el servidor de Hola donde va a instalar el conector de hello, quizás no pueda ver pantalla de registro de bienvenida. acceso de tooget, siga las instrucciones de hello en el mensaje de error de saludo. Asegúrese de que Internet Explorer Enhanced Security está desactivado.

Si desea tener alta disponibilidad, debe implementar al menos dos conectores. Cada conector debe estar registrado de manera independiente.

## <a name="test-that-hello-connector-installed-correctly"></a>Probar dicho conector Hola instalado correctamente

Puede confirmar que un nuevo conector instalado correctamente mediante la comprobación en cualquier portal de Azure de Hola o en el servidor. 

En Hola portal de Azure, inicie sesión en el inquilino de tooyour y navegar demasiado**Azure Active Directory** > **Proxy de aplicación**. Todos los conectores y grupos de conectores aparecen en esta página. Seleccione un conector toosee sus detalles o muévalo a un grupo de conectores diferentes. 

En el servidor, compruebe la lista de hello de servicios de activos para el conector de Hola y actualizador del conector Hola. dos servicios de Hello deberían empezar a ejecutarse inmediatamente, pero si no es así, activarlos: 

   * **Conector de Proxy de aplicación de Microsoft AAD** habilita la conectividad

   * **Actualizador del conector del proxy de aplicación de Microsoft AAD** es un servicio de actualización automática. Actualizador de Hello comprueba si hay nuevas versiones del conector de Hola y actualizaciones Hola conector según sea necesario.

   ![Servicios de conector del proxy de la aplicación (captura de pantalla)](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Para obtener información acerca de cómo mantienen actualizados toodate y conectores, consulte [conectores de Proxy de aplicación de AD de Azure comprender](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Pasos siguientes
Ya estás listo demasiado[publicar aplicaciones con Proxy de aplicación](application-proxy-publish-azure-portal.md).

Si tiene aplicaciones que se encuentran en redes independientes o en distintas ubicaciones, usar el conector de grupos de conectores distintos de tooorganize hello en unidades lógicas. Obtenga más información sobre cómo [trabajar con conectores de Proxy de aplicación](active-directory-application-proxy-connectors-azure-portal.md).
