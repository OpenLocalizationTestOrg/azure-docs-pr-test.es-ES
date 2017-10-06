---
title: "aaaAccess API de servicios multimedia de Azure con la autenticación de Active Directory de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de conceptos y los pasos tootake toouse Azure Active Directory (Azure AD) tooauthenticate acceso toohello API de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Hola de acceso a API de servicios multimedia de Azure con autenticación de Azure AD
 
Hola API de servicios multimedia de Azure es una API de REST. Puede utilizar lo tooperform operaciones en recursos multimedia a través de una API de REST o mediante el SDK de cliente disponibles. Azure Media Services ofrece un SDK del cliente de Media Services para Microsoft .NET. toobe había autorizado hello API de servicios multimedia y recursos de servicios multimedia de tooaccess, primero se debe autenticar. 

Media Services admite la [autenticación basada en Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md). Hola servicio REST de multimedia de Azure requiere que el usuario de Hola o una aplicación que realiza las solicitudes de API de REST de hello tengan cualquier hello **colaborador** o **propietario** rol tooaccess Hola recursos. Para obtener más información, consulte [empezar a trabajar con Control de acceso basado en roles en el portal de Azure hello](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Actualmente, servicios multimedia admite el modelo de autenticación de servicio de Control de acceso de Azure Hola. Sin embargo, la autorización de Access Control dejará de usarse el 1 de junio de 2018. Se recomienda que migre modelo de autenticación de Azure AD toohello tan pronto como sea posible.

Este documento proporciona información general sobre cómo tooaccess Hola API de servicios multimedia mediante API de .NET o REST.

## <a name="access-control"></a>Control de acceso

Para toosucceed de solicitud de REST de multimedia de Azure de hello, usuario que realiza la llamada de hello debe tener un rol de propietario o colaborador para la cuenta de servicios multimedia está intentando tooaccess Hola.  
Puede permitir que sólo un usuario con rol de propietario de hello medios recursos (cuenta) de acceso toonew los usuarios o aplicaciones. rol de colaborador de Hello puede tener acceso a recurso multimedia de hello solo.
Las solicitudes no autorizadas producirán un error, con el código de estado 401. Si ve este código de error, compruebe si el usuario tiene Hola colaborador o rol de propietario asignado para la cuenta de usuario de hello de servicios multimedia. Puede comprobarlo en hello portal de Azure. Busque la cuenta de multimedia y, a continuación, haga clic en hello **el control de acceso** ficha. 

![Pestaña Control de acceso](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Tipos de autenticación 
 
Al utilizar la autenticación de Azure AD con Azure Media Services, tiene dos opciones de autenticación:

- **Autenticación de usuario**. Autenticar a una persona que usa Hola aplicación toointeract con recursos de servicios multimedia. aplicación interactiva de Hello en primer lugar debe pedir a Hola usuario las credenciales de usuario de Hola. Un ejemplo es una aplicación de consola de administración que usan los trabajos de codificación de los usuarios autorizados toomonitor o streaming en directo. 
- **Autenticación de entidad de servicio**. Autenticar un servicio. Las aplicaciones que normalmente utilizan este método de autenticación son las que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados. Algunos ejemplos son las Web Apps, las Function Apps, las Logic Apps, las API y los microservicios.

### <a name="user-authentication"></a>Autenticación de usuarios 

Las aplicaciones que se deben usar el método de autenticación de usuario de hello son la administración o supervisión de aplicaciones nativas: aplicaciones móviles, las aplicaciones de Windows y aplicaciones de consola. Este tipo de solución es útil cuando desee que la interacción humana con el servicio de hello en uno de hello los escenarios siguientes:

- Panel de supervisión para los trabajos de codificación.
- Panel de supervisión para Live Stream.
- Aplicación de administración de recursos de tooadminister de los usuarios de escritorio o portátil en una cuenta de servicios multimedia.

> [!NOTE]
> Este método de autenticación no debe usarse para las aplicaciones orientadas al consumidor. 

Una aplicación nativa debe adquirir primero un token de acceso de Azure AD y, a continuación, usarla al realizar la API de REST de servicios de multimedia toohello de las solicitudes HTTP. Agregar encabezado de solicitud de token toohello Hola acceso. 

Hola siguiente diagrama muestra un flujo de autenticación de aplicación interactiva típica: 

![Diagrama de aplicaciones nativas](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

Hola anterior diagrama, Hola números representan flujo Hola de solicitudes de hello en orden cronológico.

> [!NOTE]
> Cuando se usa el método de autenticación de usuario de hello, todas las aplicaciones comparten Hola mismo Id. de cliente de aplicación nativa (valor predeterminado) y la aplicación nativa de URI de redireccionamiento. 

1. Pida al usuario las credenciales.
2. Solicitar un token de acceso de Azure AD con hello parámetros siguientes:  

    * Punto de conexión de inquilino de Azure AD.

        puede recuperar la información de inquilino de Hola de hello portal de Azure. Coloque el cursor sobre el nombre de usuario que inició sesión Hola Hola en la esquina superior derecha de Hola.
    * URI del recurso de Media Services. 

        Este URI se Hola igual para las cuentas de servicios multimedia que se encuentran en hello mismo entorno de Azure (por ejemplo, https://rest.media.azure.net).

    * Id. de cliente de aplicación de Media Services (nativo).
    * URI de redireccionamiento de aplicación de Media Services (nativo).
    * URI del recurso de Media Services de REST.
        
        Hola URI representa el extremo de la API de REST de hello (por ejemplo, https://test03.restv2.westus.media.azure.net/api/).

    tooget valores para estos parámetros, consulte [usar la configuración de autenticación de Azure tooaccess portal Azure AD hello](media-services-portal-get-started-with-aad.md) mediante la opción de autenticación de usuario de Hola.

3. token de acceso de Azure AD Hola se envía a toohello cliente.
4. cliente de Hola envía una solicitud toohello API de REST de multimedia de Azure con el token de acceso de hello Azure AD.
5. cliente de Hello vuelve datos hello de servicios multimedia.

Para obtener información acerca de cómo toocommunicate de autenticación toouse Azure AD con REST se solicita mediante el uso de SDK de cliente de .NET de los servicios multimedia de hello, consulte [tooaccess de autenticación de uso de Azure AD Hola API de servicios multimedia con .NET](media-services-dotnet-get-started-with-aad.md). 

Si no utiliza el SDK de cliente de .NET de los servicios multimedia de hello, debe crear manualmente una solicitud de token de acceso de Azure AD mediante el uso de parámetros de hello descritos en el paso 2. Para obtener más información, consulte [cómo toouse hello Azure AD biblioteca de autenticación tooget Hola token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Autenticación de entidad de servicio

Las aplicaciones que normalmente utilizan este método de autenticación son las que ejecutan servicios de nivel intermedio o trabajos programados: Web Apps, Function Apps, Logic Apps, API o microservicios. Este método de autenticación también es adecuado para las aplicaciones interactivas en los que podría querer toouse una cuenta de servicio toomanage recursos.

Cuando usas escenarios de consumidor de hello servicio autenticación principal método toobuild, autenticación normalmente se controla en el nivel intermedio de hello (a través de algunas API) y no directamente en una aplicación de escritorio o móvil. 

toouse este método, cree una aplicación de Azure AD y entidad de seguridad en su propio inquilino de servicio. Después de crear la aplicación hello, proporcionan Hola aplicación propietario o colaborador de rol acceso toohello cuenta de servicios multimedia. Puede hacerlo en hello portal de Azure, mediante la CLI de Azure, o con un script de PowerShell. También puede usar una aplicación de Azure AD existente. Se pueden registrar y administrar la aplicación de Azure AD y el servicio principal [Hola portal de Azure](media-services-portal-get-started-with-aad.md). También puede usar la [CLI de Azure 2.0](media-services-use-aad-auth-to-access-ams-api.md) o [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Aplicaciones de nivel intermedio](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Después de crear la aplicación de Azure AD, se obtienen valores de hello después de la configuración. Necesitará estos valores para la autenticación:

- id. de cliente 
- Secreto del cliente 

Hola anterior figura, Hola números representan flujo Hola de solicitudes de hello en orden cronológico:
    
1. Una aplicación de nivel intermedio (API de web o aplicación web) solicita un token de acceso de Azure AD que tenga Hola parámetros siguientes:  

    * Punto de conexión de inquilino de Azure AD.

        puede recuperar la información de inquilino de Hola de hello portal de Azure. Coloque el cursor sobre el nombre de usuario que inició sesión Hola Hola en la esquina superior derecha de Hola.
    * URI del recurso de Media Services. 

        Este URI se Hola igual para las cuentas de servicios multimedia que se encuentran en hello mismo entorno de Azure (por ejemplo, https://rest.media.azure.net).

    * URI del recurso de Media Services de REST.

        Hola URI representa el extremo de la API de REST de hello (por ejemplo, https://test03.restv2.westus.media.azure.net/api/).

    * Los valores de aplicación de Azure AD: Hola Id. de cliente y el secreto del cliente.
    
    tooget valores para estos parámetros, consulte [usar la configuración de autenticación de Azure tooaccess portal Azure AD hello](media-services-portal-get-started-with-aad.md) utilizando la opción de autenticación principal de servicio de Hola.

2. token de acceso de Azure AD Hola se envía toohello de nivel intermedio.
4. nivel intermedio de Hello envía solicitud toohello API de REST de multimedia de Azure con el token de hello Azure AD.
5. nivel intermedio de Hello vuelve datos hello de servicios multimedia.

Para obtener más información acerca de cómo toocommunicate de autenticación toouse Azure AD con REST se solicita mediante el uso de SDK de cliente de .NET de los servicios multimedia de hello, consulte [tooaccess de autenticación de uso de Azure AD API de servicios multimedia de Azure con .NET](media-services-dotnet-get-started-with-aad.md). 

Si no utiliza el SDK de cliente de .NET de los servicios multimedia de hello, debe crear manualmente una solicitud de token de Azure AD mediante el uso de parámetros que se describen en el paso 1. Para obtener más información, consulte [cómo toouse hello Azure AD biblioteca de autenticación tooget Hola token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Solución de problemas

Excepción: "servidor remoto hello devolvió un error: no autorizado (401)."

Solución: Para toosucceed de solicitud de REST de servicios multimedia de hello, usuario que realiza la llamada de hello debe ser un rol de colaborador o propietario en hello cuenta de servicios multimedia está tratando de tooaccess. Para obtener más información, vea hello [el control de acceso](media-services-use-aad-auth-to-access-ams-api.md#access-control) sección.

## <a name="resources"></a>Recursos

Hola siguientes artículos es información general de conceptos de autenticación de Azure AD: 

- [Escenarios de autenticación abordados por Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Incorporación, actualización o eliminación de una aplicación en Azure AD](../active-directory/develop/active-directory-integrating-applications.md)
- [Configuración y administración del control de acceso basado en rol con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Pasos siguientes

* Usar hello portal de Azure demasiado[acceso tooconsume de autenticación de Azure AD API de servicios multimedia de Azure](media-services-portal-get-started-with-aad.md).
* Utilizar autenticación de Azure AD demasiado[acceso a API de servicios multimedia de Azure con .NET](media-services-dotnet-get-started-with-aad.md).

