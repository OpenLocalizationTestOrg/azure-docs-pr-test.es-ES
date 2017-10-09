---
title: "aaaGet inició con autenticación de Azure AD mediante Hola portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure tooaccess portal tooconsume de autenticación de Azure Active Directory (Azure AD) Hola API de servicios multimedia de Azure."
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Empezar a trabajar con autenticación de Azure AD mediante el uso de hello portal de Azure

Obtenga información acerca de cómo toouse hello Azure tooaccess portal Azure Active Directory (Azure AD) autenticación tooaccess Hola API de servicios multimedia de Azure.

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta de Azure. Si no tiene cuenta, comience con una [evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Una cuenta de Media Services. Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de Hola](media-services-portal-create-account.md).
- Asegúrese de revisar hello [obtiene acceso a la API de los servicios de multimedia de Azure con información general de autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

Al utilizar la autenticación de Azure AD con Azure Media Services, tiene dos opciones de autenticación:

- **Autenticación de usuario**. Autenticar a una persona que usa Hola aplicación toointeract con recursos de servicios multimedia. aplicación interactiva de Hello en primer lugar debe solicitarle las credenciales de usuario Hola. Un ejemplo es una aplicación de consola de administración que usan los trabajos de codificación de los usuarios autorizados toomonitor o streaming en directo. 
- **Autenticación de entidad de servicio**. Autenticar un servicio. Las aplicaciones que normalmente utilizan este método de autenticación son aplicaciones que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados: Web Apps, Function Apps, Logic Apps, API o un microservicio.

> [!IMPORTANT]
> Actualmente, servicios multimedia admite el modelo de autenticación de servicio de Control de acceso de Azure Hola. Sin embargo, la autorización de Access Control dejará de usarse el 1 de junio de 2018. Se recomienda que migre modelo de autenticación de Azure AD toohello tan pronto como sea posible.

## <a name="select-hello-authentication-method"></a>Seleccionar método de autenticación de Hola

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia.
2. Seleccione cómo tooconnect toohello API de servicios multimedia.

    ![Página de selección del método de conexión](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Autenticación de usuarios

Hola a tooconnect toohello API de servicios multimedia mediante el uso de la opción de autenticación de usuario, la aplicación de cliente de hello debe toorequest un token de Azure AD que ha Hola parámetros siguientes:  

* Punto de conexión de inquilino de Azure AD
* URI del recurso de Media Services
* Id. de cliente de aplicación de Media Services (nativo) 
* URI de redireccionamiento de aplicación de Media Services (nativo) 
* URI del recurso de Media Services de REST

Puede obtener valores de hello para estos parámetros en hello **API de servicios multimedia con la autenticación de usuario** página. 

![Página de conexión con la autenticación de usuario](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Si se conecta toohello API de servicios multimedia mediante el uso de hello Media Services Microsoft .NET SDK, Hola requiere valores son tooyou disponible como parte del SDK de Hola. Para obtener más información, consulte [tooaccess de autenticación de uso de Azure AD Hola API de servicios multimedia de Azure con .NET](media-services-dotnet-get-started-with-aad.md).

Si no está usando el SDK de cliente de .NET de los servicios multimedia de hello, debe crear manualmente una solicitud de token de Azure AD mediante parámetros de Hola que se analizaron anteriormente. Para obtener más información, consulte [cómo toouse hello Azure AD biblioteca de autenticación tooget Hola token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Autenticación de entidad de servicio

tooconnect toohello API de servicios multimedia mediante el uso de Hola opción principal de servicio, la aplicación de nivel intermedio (API de web o aplicación web) debe toorequest un token de Azure AD que ha Hola parámetros siguientes:  

* Punto de conexión de inquilino de Azure AD
* URI del recurso de Media Services 
* URI del recurso de Media Services de REST
* Los valores de aplicación de Azure AD: Hola **Id. de cliente** y **secreto de cliente**

Puede obtener valores de hello para estos parámetros en hello **conectar tooMedia API de servicios con la entidad de servicio** página. Utilice este toocreate página un nuevo Azure aplicación AD o tooselect uno ya existente. Después de seleccionar la aplicación de Azure AD de hello, puede obtener identificador de cliente de hello (Id. de aplicación) y generar valores de hello cliente secreto (clave). 

![Página de conexión a la entidad de servicio](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Cuando Hola **entidad de servicio** hoja se abre, se selecciona la primera aplicación de Azure AD de Hola que cumpla Hola siguiendo criterios:

- Se trata de una aplicación registrada de Azure AD.
- Permisos de Control de acceso de Owner Role-Based o colaborador tiene en cuenta Hola.

Después de crear o seleccionar una aplicación de Azure AD, puede crear y copiar un secreto de cliente (clave) y Hola Id. de cliente (identificador de aplicación). Identificador de cliente y secreto de cliente Hello son el token de acceso de hello tooget necesario en este escenario.

Si no tiene aplicaciones de Azure AD de toocreate de permisos en el dominio, no se muestran los controles de la aplicación hello Azure AD de hoja de Hola y se muestra un mensaje de advertencia.

Si se conecta toohello API de servicios multimedia mediante el uso de hello Media Services .NET SDK, vea [tooaccess de autenticación de uso de Azure AD Hola API de servicios multimedia de Azure con .NET](media-services-dotnet-get-started-with-aad.md).

Si no utiliza el SDK de cliente de .NET de los servicios multimedia de hello, debe crear manualmente una solicitud de token de Azure AD con parámetros de Hola que se analizaron anteriormente. Para obtener más información, consulte [cómo toouse hello Azure AD biblioteca de autenticación tooget Hola token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Obtener a cliente hello secreto de cliente y el Id.

Después de seleccionar una aplicación de Azure AD existente u Hola seleccione opción toocreate uno nuevo, aparece Hola siguientes botones:

![Botón Administrar permisos y botón Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

Hola tooopen hoja de aplicaciones de Azure AD, haga clic en **administrar aplicación**. En hello **administrar aplicación** hoja, puede obtener el identificador de cliente de la aplicación hello (Id. de aplicación). toogenerate un secreto de cliente (clave), seleccione **claves**.

![Opción Claves de la hoja Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Administrar los permisos y la aplicación hello

Después de seleccionar la aplicación de Azure AD de hello, puede administrar permisos y la aplicación hello. tooset seguridad su tooaccess de aplicación de Azure AD otras aplicaciones, haga clic en **administrar permisos**. Para las tareas de administración, como el cambio de claves y direcciones URL de respuesta o tooedit Hola manifiesto de aplicación, haga clic en **administrar aplicación**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Editar la configuración de la aplicación hello o en el manifiesto

aplicación de hello tooedit valores de configuración o manifiesto, haga clic en **administrar aplicación**.

![Página de Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-portal-upload-files.md).
