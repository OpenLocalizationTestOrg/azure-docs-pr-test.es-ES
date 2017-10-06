---
title: "Azure AD Connect: Certificado actualización Hola SSL para una granja de servidores de servicios de federación de Active Directory (AD FS) | Documentos de Microsoft"
description: Este documento detalles Hola pasos tooupdate Hola certificado SSL de una granja de AD FS mediante el uso de Azure AD Connect.
services: active-directory
keywords: "azure ad connect, actualizar ssl de adfs, actualizar certificado de adfs, cambiar certificado de adfs, nuevo certificado de adfs, certificado de adfs, actualizar certificado ssl de adfs, actualizar certificado ssl de adfs, configurar certificado ssl de adfs, adfs, ssl, certificado, certificado de comunicación de servicio de adfs, actualizar federación, configurar federación, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Actualiza el certificado SSL de Hola para una granja de servidores de servicios de federación de Active Directory (AD FS)

## <a name="overview"></a>Información general
Este artículo describe cómo se puede usar certificado SSL de Azure AD Connect tooupdate hello en una granja de servidores de servicios de federación de Active Directory (AD FS). Puede usar certificado de hello Azure AD Connect herramienta tooeasily actualización Hola SSL de granja de servidores de hello AD FS aunque Hola inicio de sesión en método de usuario seleccionado no está AD FS.

Puede realizar toda la operación de actualización de certificado SSL para la granja de servidores de hello AD FS a través de todos los servidores de Proxy de aplicación Web (WAP) en tres pasos sencillos y federación hello:

![Tres pasos](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn más información acerca de los certificados usados por AD FS, consulte [descripción de los certificados usados por AD FS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Requisitos previos

* **Granja de AD FS**: asegúrese de que la granja de AD FS se base en Windows Server 2012 R2 o una versión posterior.
* **Azure AD Connect**: asegúrese de que Hola versión de Azure AD Connect es 1.1.443.0 o posterior. Va a utilizar la tarea hello **actualización AD el certificado SSL FS**.

![Tarea de actualización de SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Paso 1: Proporcionar información de la granja de AD FS

Azure AD Connect intenta automáticamente tooobtain información acerca de la granja de servidores de hello AD FS:
1. Consultar información de la granja de servidores de Hola de AD FS (Windows Server 2016 o posterior).
2. Hacer referencia a información de Hola de ejecuciones anteriores, que se almacenan de forma local con Azure AD Connect.

Puede modificar la lista de Hola de servidores que se muestran agregando o quitando hello tooreflect Hola actual configuración de servidores de granja de servidores de hello AD FS. Tan pronto como se proporciona la información del servidor hello, Azure AD Connect muestra conectividad de Hola y el estado de certificados SSL actual.

![Información del servidor de AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Si la lista de hello contiene un servidor que ya no forma parte de la granja de servidores de hello AD FS, haga clic en **quitar** toodelete servidor de hello en lista de Hola de servidores en la granja de servidores de AD FS.

![Servidor sin conexión en la lista](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Quitar un servidor de la lista de Hola de servidores de AD FS de granja de servidores en Azure AD Connect es una operación local y las actualizaciones de Hola información de hello granja de AD FS que Azure AD Connect mantiene localmente. Azure AD Connect no modifica la configuración de hello en AD FS tooreflect Hola cambio.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Paso 2: Proporcionar el nuevo certificado SSL

Cuando haya confirmado información Hola acerca de los servidores de la granja de servidores de AD FS, Azure AD Connect solicita nuevo certificado SSL de Hola. Proporcione una protección por contraseña PFX toocontinue Hola instalación del certificado.

![Certificado SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Después de proporcionar el certificado de hello, Azure AD Connect pasa por una serie de requisitos previos. Comprobar Hola certificado tooensure que Hola certificado es correcto para la granja de servidores de AD FS hello:

-   Hello nombre de asunto de nombre/alternativo de sujeto de certificado de hello es Hola igual como nombre de servicio de federación de hello, o es un certificado comodín.
-   certificado de Hello es válido durante más de 30 días.
-   cadena de confianza del certificado de Hello es válido.
-   certificado de Hello está protegido con contraseña.

## <a name="step-3-select-servers-for-hello-update"></a>Paso 3: Seleccione los servidores de actualización de Hola

En el paso siguiente de hello, seleccione servidores de Hola que necesitan toohave Hola SSL certificado actualizado. Actualización de hello no se puede seleccionar los servidores que están sin conexión.

![Seleccione los servidores tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Después de completar la configuración de hello, Azure AD Connect muestra mensajes de Hola que indica el estado de saludo de la actualización de Hola y proporciona un inicio de sesión de AD FS hello tooverify de opción.

![Configuración completada](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>Preguntas más frecuentes

* **¿Qué debe ser el nombre de asunto Hola del certificado de Hola Hola nuevo certificado de SSL de AD FS?**

    Azure AD Connect comprueba si Hola sujeto alternativo de nombre/nombre del firmante Hola certificado contiene nombre de servicio de federación de Hola. Por ejemplo, si el nombre de servicio de federación es fs.contoso.com, el nombre de sujeto alternativo/nombre de sujeto de hello debe ser fs.contoso.com.  También se aceptan certificados comodín.

* **¿Por qué se me pide las credenciales de nuevo en la página del servidor WAP Hola?**

    Si las credenciales de Hola que proporcione para conectarse a servidores de FS tooAD también no tienen los servidores WAP Hola privilegio toomanage hello, Azure AD Connect pide las credenciales que tienen privilegios administrativos en los servidores WAP Hola.

* **servidor de Hola se muestra como sin conexión. ¿qué debo hacer?**

    Azure AD Connect no puede realizar cualquier operación si Hola servidor está sin conexión. Si Hola servidor forma parte de hello granja de AD FS, a continuación, compruebe el servidor de toohello de conectividad de Hola. Después de resolver el problema de hello, presione Hola actualizar icono tooupdate Hola estado Asistente Hola. Si el servidor de hello formaba parte de hello granja anteriormente pero ahora ya no existe, haga clic en **quitar** toodelete de lista de Hola de servidores que se conectan de Azure AD mantiene. Quitar servidor hello en lista de hello en Azure AD Connect no altera Hola configuración de AD FS propio. Si usa AD FS en Windows Server 2016 o posterior, sigue siendo de servidor hello en los valores de configuración de Hola y se mostrará nuevo hello vuela hello tarea se ejecuta.

* **¿Se puede actualizar un subconjunto de Mis servidores de granja de servidores con un certificado SSL nuevo Hola?**

    Sí. Siempre puede ejecutar la tarea hello **certificado SSL de actualización** nuevo Hola de tooupdate servidores restantes. En hello **actualización de certificados de servidores seleccionados para SSL** página, puede ordenar la lista Hola de servidores en **fecha de expiración de SSL** tooeasily acceder a servidores de Hola que aún no se actualizó.

* **Quita servidor de Hola Hola anterior que se ejecuta, pero se sigue que se muestra como sin conexión y se muestra en la página de hello AD FS servidores. ¿Por qué es servidor de sin conexión de hello estando disponibles incluso después de que quitó?**

    Quitar servidor hello en lista de hello en Azure AD Connect no quitarlo en hello configuración de AD FS. AD FS (Windows Server 2016 o posterior) para toda la información acerca de la granja de servidores de hello hace referencia a Azure AD Connect. Si servidor hello sigue estando presente en hello configuración de AD FS, se enumerarán en la lista de Hola.  

## <a name="next-steps"></a>Pasos siguientes

- [Azure AD Connect y la federación](active-directory-aadconnectfed-whatis.md)
- [Servicios de federación de Active Directory y personalización con Azure AD Connect](active-directory-aadconnect-federation-management.md)
