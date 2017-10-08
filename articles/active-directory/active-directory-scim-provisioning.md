---
title: "aaaUsing sistema de administración de identidades entre dominios aprovisionar automáticamente a los usuarios y grupos de Azure Active Directory tooapplications | Documentos de Microsoft"
description: "Azure Active Directory pueda aprovisionar automáticamente a los usuarios y grupos tooany identidad o aplicación almacén que está representado por un servicio web con interfaz Hola definido en la especificación del protocolo SCIM Hola"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>Usa el sistema para los usuarios de administración de identidades entre dominios tooautomatically aprovisionar y grupos de Azure Active Directory tooapplications

## <a name="overview"></a>Información general
Azure Active Directory (Azure AD) pueden aprovisionar automáticamente a los usuarios y grupos tooany identidad o aplicación almacén que está representado por un servicio web con interfaz de hello definida en hello [System para entre dominios Identity Management (SCIM) 2.0 especificación del protocolo](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory puede enviar solicitudes toocreate, modificar o eliminar asignado servicio de web toohello usuarios y grupos. servicio web de Hello, a continuación, puede convertir las solicitudes en las operaciones en el almacén de identidades de destino de Hola. 

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. 



![][0]
*Figura 1: Aprovisionamiento de almacén de identidades de Azure Active Directory tooan a través de un servicio web*

Esta capacidad se puede utilizar junto con capacidad de "traiga su propia aplicación" hello en Azure AD tooenable single sign-on y para las aplicaciones que proporcionan o representadas por un servicio web SCIM el aprovisionamiento automático de usuarios.

Existen dos casos de uso de SCIM en Azure Active Directory:

* **Aprovisionamiento de usuarios y grupos tooapplications que admiten SCIM** aplicaciones que admiten SCIM 2.0 y usar tokens de portador OAuth para la autenticación funciona con Azure AD sin necesidad de configuración.
* **Crear su propia solución de aprovisionamiento de aplicaciones compatibles con otros aprovisionamiento basado en la API** para las aplicaciones no SCIM, puede crear un tootranslate de punto de conexión SCIM entre el punto de conexión de Azure AD SCIM hello y cualquier aplicación de Hola de API es compatible con para el aprovisionamiento de usuario. toohelp desarrollar un punto de conexión SCIM, se proporcionan las bibliotecas de Common Language Infrastructure (CLI) junto con ejemplos de código que muestran cómo toodo proporcionan un punto de conexión SCIM y traducir los mensajes de SCIM.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Aprovisionamiento de usuarios y grupos tooapplications que admiten SCIM
Azure AD puede ser configurado tooautomatically aprovisionar asignado a los usuarios y grupos tooapplications que implementan un [sistema de administración de identidades entre dominios 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) servicio web y acepta los tokens de portador de OAuth para la autenticación . Dentro de la especificación de hello SCIM 2.0, las aplicaciones deben cumplir estos requisitos:

* Admite la creación de usuarios o grupos, según la sección 3.3 de hello protocolo SCIM.  
* Admite la modificación de los usuarios o grupos con las solicitudes de revisión según la sección 3.5.2 de hello protocolo SCIM.  
* Admite la recuperación de un recurso conocido según la sección 3.4.1 de hello protocolo SCIM.  
* Admite consultas de usuarios o grupos, de acuerdo con el punto 3.4.2 de hello protocolo SCIM.  De forma predeterminada, los usuarios se consultan por externalId y los grupos por displayName.  
* Admite consultas de usuario con el identificador y Administrador de acuerdo con el punto 3.4.2 de hello protocolo SCIM.  
* Permite consultar los grupos por Id. y miembro según la sección 3.4.2 de hello protocolo SCIM.  
* Acepta los tokens de portador de OAuth para la autorización según la sección 2.1 de hello protocolo SCIM.

Consulte a su proveedor de la aplicación o la documentación que se incluye con la aplicación para ver si existen declaraciones de compatibilidad con estos requisitos.

### <a name="getting-started"></a>Introducción
Las aplicaciones que admiten el perfil SCIM Hola se describe en este artículo pueden ser conectado tooAzure Active Directory mediante la característica de "aplicación distinta de la Galería" hello en Galería de aplicaciones de hello Azure AD. Una vez conectado, Azure AD se ejecuta un proceso de sincronización cada 20 minutos donde consulta punto de conexión de la aplicación hello SCIM para asigna usuarios y grupos y crea o modifica ellos según toohello detalles de asignación.

**una aplicación que admita SCIM tooconnect:**

1. Inicie sesión en demasiado[Hola portal de Azure](https://portal.azure.com). 
2. Examinar demasiado ** Azure Active Directory > aplicaciones empresariales y seleccione **nueva aplicación > todos los > aplicación no gallery**.
3. Escriba un nombre para la aplicación y haga clic en **agregar** icono toocreate un objeto de aplicación.
    
  ![][1]
  *Figura 2: galería de aplicaciones de Azure AD*
    
4. En la pantalla resultante de bienvenida, seleccione hello **Provisioning** pestaña en la columna izquierda de Hola.
5. Hola **modo de aprovisionamiento** menú, seleccione **automática**.
    
  ![][2]
  *Figura 3: Configurar el aprovisionamiento en hello portal de Azure*
    
6. Hola **dirección URL del inquilino** , escriba la dirección URL de Hola de punto de conexión de la aplicación hello SCIM. Ejemplo: https://api.contoso.com/scim/v2/
7. Si el punto de conexión de hello SCIM requiere un token de portador de OAuth de un emisor que no sea de Azure AD, Hola copia requeridos token de portador OAuth en hello opcional **secreto Token** campo. Si este campo se deja en blanco, Azure AD incluye un token de portador OAuth emitido desde Azure AD con cada solicitud. Las aplicaciones que usan Azure AD como un proveedor de identidades pueden validar este token emitido por Azure AD.
8. Haga clic en hello **Probar conexión** botón toohave Azure Active Directory intento tooconnect toohello SCIM punto de conexión. Si se produce un error en los intentos de hello, se muestra información de error.  
9. Si Hola intentos tooconnect toohello aplicación se realiza correctamente, a continuación, haga clic en **guardar** credenciales de administrador de toosave Hola.
10. Hola **asignaciones** sección, hay dos conjuntos seleccionables de asignaciones de atributos: uno para objetos de usuario y otro para los objetos de grupo. Seleccione cada uno atributos de Hola de tooreview que se sincronizan desde la aplicación de Azure Active Directory tooyour. Hola atributos seleccionados como **coincidencia** propiedades son utilizados toomatch Hola usuarios y grupos en su aplicación para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

    >[!NOTE]
    >Opcionalmente, puede deshabilitar la sincronización de objetos de grupo deshabilitando Hola "grupos" asignación. 

11. En **configuración**, hello **ámbito** campo define qué usuarios y grupos están sincronizados. Al seleccionar "Sincronización solo asigna usuarios y grupos" (recomendado) solo sincronizará los usuarios y grupos asignados en hello **usuarios y grupos** ficha.
12. Una vez completada la configuración, cambiar hello **estado de aprovisionamiento** demasiado**en**.
13. Haga clic en **guardar** toostart Hola servicio de aprovisionamiento de Azure AD. 
14. Si sincronizar solo asigna usuarios y grupos (recomendados), ser seguro hello tooselect **usuarios y grupos** pestaña y asigne los usuarios de Hola o grupos que desea toosync.

Una vez que se inició la sincronización inicial de hello, puede usar hello **registros de auditoría** ficha toomonitor progreso, que muestra todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación. Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Creación de una solución de aprovisionamiento propia para cualquier aplicación
Al crear un servicio web SCIM que interactúa con Azure Active Directory, puede habilitar el inicio de sesión único y el aprovisionamiento automático de usuarios para prácticamente cualquier aplicación que proporciona una API de aprovisionamiento de usuarios REST o SOAP.

Aquí le mostramos cómo funciona:

1. Azure AD proporciona una biblioteca de infraestructura de lenguaje común conocida como [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Los desarrolladores e integradores de sistema pueden usar esta biblioteca toocreate e implementar un extremo de servicio web basado en SCIM capaz de conectar el almacén de identidades de la aplicación de Azure AD tooany.
2. Las asignaciones se implementan en hello web servicio toomap Hola usuario estandarizado toohello usuario de esquema y protocolo requerido por la aplicación hello.
3. dirección URL del extremo Hola está registrado en Azure AD como parte de una aplicación personalizada en la Galería de aplicaciones de Hola.
4. Usuarios y grupos se asignan toothis aplicación en Azure AD. Tras la asignación, se colocan en una aplicación de destino de cola toobe sincronizado toohello. proceso de sincronización de Hello control cola Hola se ejecuta cada 20 minutos.

### <a name="code-samples"></a>Ejemplos de código
toomake esto, procesar un conjunto de [ejemplos de código](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) son siempre que cree un extremo del servicio web SCIM y demostrar el aprovisionamiento automático. Uno de los ejemplos es de un proveedor que mantiene un archivo con filas de valores separados por comas que representan a usuarios y grupos.  Hola otro es de un proveedor que funciona en el servicio de Amazon Web Services Identity and Access Management Hola.  

**Requisitos previos**

* Visual Studio 2013 o posterior.
* [SDK de Azure para .NET](https://azure.microsoft.com/downloads/)
* Equipo de Windows que admita Hola ASP.NET framework 4.5 toobe utiliza como Hola extremo SCIM. Este equipo debe ser accesible desde la nube de Hola
* [Una suscripción de Azure con una versión de prueba o con licencia de Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* ejemplo de Hola a Amazon AWS requiere bibliotecas de hello [AWS Toolkit para Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Para obtener más información, vea Hola Léame archivo incluido con el ejemplo de Hola.

### <a name="getting-started"></a>Introducción
tooimplement Hola de manera más fácil solicita un punto de conexión SCIM que puede aceptar el aprovisionamiento de Azure AD es toobuild e implementar el ejemplo de código de hello que genera el archivo de valores separados por comas (CSV) de hello los usuarios aprovisionados tooa.

**un punto de conexión de ejemplo SCIM toocreate:**

1. Descargar paquete de ejemplo de código de hello en [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Descomprima el paquete de Hola y lo coloca en el equipo de Windows en una ubicación como C:\AzureAD-BYOA-Provisioning-Samples\.
3. En esta carpeta, iniciar solución de FileProvisioningAgent de hello en Visual Studio.
4. Seleccione **Herramientas > Administrador de paquetes de biblioteca > Package Manager Console**y ejecute hello siguientes comandos para hello FileProvisioningAgent tooresolve Hola solución las referencias del proyecto:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Compile hello FileProvisioningAgent proyecto.
6. Iniciar la aplicación de línea de comandos de hello en Windows (como administrador) y usar hello **cd** comando toochange Hola directorio tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** carpeta.
7. Ejecute hello siguiente comando, sustituyendo < dirección ip > Hola IP dirección o nombre de dominio de la máquina de Windows hello:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. En Windows en **configuración de Windows > configuración de Internet y red**, seleccione hello **Firewall de Windows > Configuración avanzada**y crear un **Inbound Rule** que permite el acceso de entrada tooport 9000.
9. Si la máquina de Windows hello está detrás de un enrutador, Hola enrutador necesidades toobe configurado tooperform traducción de acceso de red entre su puerto 9000 que está expuesto toohello internet y el puerto 9000 en la máquina de Windows hello. Esto es necesario para Azure AD toobe puede tooaccess este punto de conexión en la nube de Hola.

**extremo de SCIM del ejemplo de Hola tooregister en Azure AD:**

1. Inicie sesión en demasiado[Hola portal de Azure](https://portal.azure.com). 
2. Examinar demasiado ** Azure Active Directory > aplicaciones empresariales y seleccione **nueva aplicación > todos los > aplicación no gallery**.
3. Escriba un nombre para la aplicación y haga clic en **agregar** icono toocreate un objeto de aplicación. objeto de aplicación Hola creado es la aplicación de destino de hello toorepresent previsto se va a aprovisionar tooand implementar punto de conexión de hello único de inicio de sesión del mismo y no solamente SCIM.
4. En la pantalla resultante de bienvenida, seleccione hello **Provisioning** pestaña en la columna izquierda de Hola.
5. Hola **modo de aprovisionamiento** menú, seleccione **automática**.
    
  ![][2]
  *Figura 4: Configurar el aprovisionamiento en hello portal de Azure*
    
6. Hola **dirección URL del inquilino** , escriba la dirección URL de hello expuesta a internet y el puerto de su punto de conexión SCIM. Esto sería algo como http://testmachine.contoso.com:9000 o http://<ip-address>:9000/, donde < dirección ip > es Hola internet expone IP dirección.  
7. Si el punto de conexión de hello SCIM requiere un token de portador de OAuth de un emisor que no sea de Azure AD, Hola copia requeridos token de portador OAuth en hello opcional **secreto Token** campo. Si se deja este campo en blanco, Azure AD incluirá un token de portador OAuth emitido desde Azure AD con cada solicitud. Las aplicaciones que usan Azure AD como un proveedor de identidades pueden validar este token emitido por Azure AD.
8. Haga clic en hello **Probar conexión** botón toohave Azure Active Directory intento tooconnect toohello SCIM punto de conexión. Si se produce un error en los intentos de hello, se muestra información de error.  
9. Si Hola intentos tooconnect toohello aplicación se realiza correctamente, a continuación, haga clic en **guardar** credenciales de administrador de toosave Hola.
10. Hola **asignaciones** sección, hay dos conjuntos seleccionables de asignaciones de atributos: uno para objetos de usuario y otro para los objetos de grupo. Seleccione cada uno atributos de Hola de tooreview que se sincronizan desde la aplicación de Azure Active Directory tooyour. Hola atributos seleccionados como **coincidencia** propiedades son utilizados toomatch Hola usuarios y grupos en su aplicación para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.
11. En **configuración**, hello **ámbito** campo define qué usuarios y grupos están sincronizados. Al seleccionar "Sincronización solo asigna usuarios y grupos" (recomendado) solo sincronizará los usuarios y grupos asignados en hello **usuarios y grupos** ficha.
12. Una vez completada la configuración, cambiar hello **estado de aprovisionamiento** demasiado**en**.
13. Haga clic en **guardar** toostart Hola servicio de aprovisionamiento de Azure AD. 
14. Si sincronizar solo asigna usuarios y grupos (recomendados), ser seguro hello tooselect **usuarios y grupos** pestaña y asigne los usuarios de Hola o grupos que desea toosync.

Una vez que se inició la sincronización inicial de hello, puede usar hello **registros de auditoría** ficha toomonitor progreso, que muestra todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación. Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

Hola último paso en la comprobación de ejemplo de Hola es tooopen hello TargetFile.csv archivo en la carpeta de \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug de hello en el equipo de Windows. Una vez que se ejecuta el proceso de aprovisionamiento de hello, este archivo muestra detalles de Hola de todo asignan y aprovisionan de usuarios y grupos.

### <a name="development-libraries"></a>Bibliotecas de desarrollo
toodevelop su propio servicio web que cumple la especificación de SCIM toohello, primero familiarizarse con hello después bibliotecas proporcionados por Microsoft toohelp acelerar el proceso de desarrollo de hello: 

1. Se ofrecen bibliotecas de Common Language Infrastructure (CLI) que se pueden usar con lenguajes basados en dicha infraestructura, como C#. Una de esas bibliotecas, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declara una interfaz Microsoft.SystemForCrossDomainIdentityManagement.IProvider, que se muestra en hello siguientes ilustración: A los desarrolladores que utilizan bibliotecas de hello implementaría esa interfaz con una clase que se puede hacer referencia, de forma genérica, como un proveedor. bibliotecas de Hello permiten Hola developer toodeploy un servicio web que cumple la especificación de SCIM toohello. servicio web de Hola o se puede hospedar en Internet Information Services o cualquier ensamblado ejecutable de Common Language Infrastructure. Solicitud se traduce a los métodos del proveedor de llamadas toohello, que se programan hello toooperate de desarrollador en un almacén de identidades.
  
  ![][3]
  
2. [Express route controladores](http://expressjs.com/guide/routing.html) están disponibles para analizar objetos de solicitud de node.js que representan llamadas (según se define en hello especificación SCIM), realizadas el servicio web de node.js de tooa.   

### <a name="building-a-custom-scim-endpoint"></a>Creación de un punto de conexión SCIM personalizado
Utilizando las bibliotecas CLI de hello, los desarrolladores que utilizan dichas bibliotecas pueden hospedar sus servicios en cualquier ensamblado de Common Language Infrastructure ejecutable, o en Internet Information Services. Este es el código de ejemplo para hospedar un servicio dentro de un ensamblado ejecutable, en la dirección de hello http://localhost: 9000: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Este servicio debe tener un certificado HTTP dirección y el servidor de autenticación del programa Hola a qué entidad de certificación raíz es uno de los siguientes de hello: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* VeriSign
* WoSign

Un certificado de autenticación de servidor puede ser puerto tooa enlazados en un host de Windows mediante la utilidad de shell de red de hello: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

En este caso, valor de Hola proporcionado para el argumento de certhash hello es huella digital de hello del certificado de hello, mientras el valor de hello proporcionado para el argumento de appid hello es un identificador único global arbitrario.  

servicio de hello toohost dentro de Internet Information Services, un desarrollador crearía un ensamblado de biblioteca de código CLA con una clase denominada inicio en hello espacio de nombres predeterminado del ensamblado de Hola.  Este es un ejemplo de este tipo de clase: 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Control de la autenticación de puntos de conexión
Las solicitudes de Azure Active Directory incluyen un token de portador de OAuth 2.0.   Cualquier solicitud de servicio receptor Hola debería autenticar el emisor de hello como Azure Active Directory en nombre del inquilino de Azure Active Directory de hello esperada para acceso toohello servicio web de Azure Active Directory Graph.  En el token de hello, emisor Hola se identifica mediante una notificación de iss, como "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".  En este ejemplo, la dirección base de hello del valor de notificación de hello, https://sts.windows.net, identifica Azure Active Directory como Hola emisor, mientras el segmento de dirección relativa, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello es un identificador único de hello Azure Active Inquilino de directorio en nombre de qué Hola token haya sido emitido.  Si Hola token haya sido emitido para el acceso a servicio de web de Azure Active Directory Graph hello, a continuación, identificador de Hola de dicho servicio, 00000002-0000-0000-c000-000000000000, debe ser en valor de Hola de aud del token de hello reclamar.  

Los desarrolladores que utilizan bibliotecas CLA Hola proporcionadas por Microsoft para la creación de un servicio SCIM pueden autenticar las solicitudes de Azure Active Directory con el paquete Microsoft.Owin.Security.ActiveDirectory de hello siguiendo estos pasos: 

1. En un proveedor, implemente la propiedad de Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior de hello haciendo que se devuelva un toobe de método que se llama cada vez que se ha iniciado el servicio de hello: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Agregue Hola después código toothat método toohave cualquier tooany de solicitud de puntos de conexión del servicio de hello autenticado como que lleven un token emitido por Azure Active Directory en nombre de un inquilino especificado para acceso toohello servicio web de Azure AD Graph: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Esquema de grupos y usuarios
Azure Active Directory puede proporcionar dos tipos de servicios web de recursos tooSCIM.  Esos tipos de recursos son los usuarios y grupos.  

Recursos de usuario se identifican por identificador de esquema de hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, que se incluye en esta especificación de protocolo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  asignación predeterminada de Hola de atributos de Hola de usuarios en los atributos de Azure Active Directory toohello de recursos de urn: ietf:params:scim:schemas:extension:enterprise:2.0:User se proporciona en la tabla 1, a continuación.  

Recursos del grupo se identifican por identificador de esquema de hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Tabla 2, a continuación, la asignación de muestra hello predeterminada de atributos de Hola de grupos de atributos de Azure Active Directory toohello de recursos http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  

### <a name="table-1-default-user-attribute-mapping"></a>Tabla 1: Asignación de atributos de usuario predeterminada
| Usuario de Azure Active Directory | urn: ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |active |
| DisplayName |DisplayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |título |
| mail |emails[type eq "work"].value |
| mailNickname |externalId |
| manager |manager |
| mobile |phoneNumbers[type eq "mobile"].value |
| objectId |id |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| surname |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>Tabla 2: Asignación de atributos de grupo predeterminada
| Grupo de Azure Active Directory  | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| DisplayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickname |DisplayName |
| members |members |
| objectId |id |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>Aprovisionamiento y cancelación del aprovisionamiento de usuarios
Hola después mensajes de saludo de la ilustración se muestra que Azure Active Directory envía tooa SCIM servicio toomanage Hola del ciclo de vida de un usuario en otro almacén de identidades. diagrama de Hello también muestra cómo SCIM proporciona un servicio implementado mediante las bibliotecas CLI de Hola por Microsoft para crear que dichos servicios traducen esas solicitudes toohello llama a métodos de un proveedor.  

![][4]
*Figura 5: secuencia de aprovisionamiento y cancelación de aprovisionamiento de usuarios*

1. Las consultas de Active Directory Azure Hola servicio para un usuario con un valor de atributo externalId que coincide con valor de atributo de hello mailNickname de un usuario en Azure AD. consulta de Hola se expresa como una solicitud de protocolo de transferencia de hipertexto (HTTP), como en este ejemplo, donde jyoung es un ejemplo de un mailNickname de un usuario en Azure Active Directory: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Si el servicio de Hola se compiló mediante bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de Hola se traduce en un método de consulta del proveedor del servicio de hello toohello de llamada.  Esta es la firma de Hola de ese método: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Aquí es definición Hola de interfaz de Hola Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters: 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  Hola siguiendo el ejemplo de una consulta para un usuario con un valor especificado para el atributo de externalId hello, valores de argumentos de hello pasados toohello método de consulta son: 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Si el servicio Hola respuesta tooa consulta toohello web para un usuario con un valor de atributo externalId que coincida con el valor de atributo mailNickname Hola de un usuario no devuelve ningún usuario, Azure Active Directory solicita que un usuario la prestación del servicio Hola correspondiente toohello uno en Azure Active Directory.  Este es un ejemplo de dicha solicitud: 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM traduciría esa solicitud en un toohello de llamada al método Create de proveedor del servicio de Hola.  método Create de Hello tiene esta firma: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  En un tooprovision de solicitud de un usuario, el valor de hello del argumento de recursos de hello es una instancia de hello Microsoft.SystemForCrossDomainIdentityManagement. Clase Core2EnterpriseUser, definido en la biblioteca de Microsoft.SystemForCrossDomainIdentityManagement.Schemas Hola.  Si el usuario de hello solicitud tooprovision Hola se realiza correctamente, a continuación, hello implementación del método hello es tooreturn esperado de una instancia de hello Microsoft.SystemForCrossDomainIdentityManagement. Core2EnterpriseUser (clase), con el valor de Hola de propiedad de identificador hello establece toohello identificador único del usuario recién suministradas Hola.  

3. tooupdate un usuario conocido tooexist en un almacén de identidades representado por un SCIM, Azure Active Directory continúa solicitando el estado actual de Hola de ese usuario del servicio Hola con una solicitud, como: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  En un servicio que se generan con bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de saludo se traduce en un método de recuperación del proveedor del servicio de hello toohello de llamada.  Esta es la firma Hola del método de recuperación de hello: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  En el ejemplo de Hola del estado actual del hello tooretrieve solicitud de un usuario, valores de hello de propiedades de hello del objeto de hello proporcionada como valor de Hola de argumento de hello parámetros son los siguientes: 
  
  * Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Si un atributo de referencia es toobe actualizado, a continuación, Azure Active Directory consultas Hola servicio toodetermine haya o no hello valor actual del atributo de referencia de hello en el almacén de identidades de hello representado por servicio Hola ya coincide con valor de Hola de dicho atributo en Azure Active Directory. Para los usuarios, Hola solo de qué hello es consultado el valor actual de esta manera es Hola manager atributo. Este es un ejemplo de una solicitud toodetermine si el atributo de administrador de Hola de un objeto de usuario determinado tiene actualmente un determinado valor: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Hola valor del parámetro de consulta de atributos de hello, identificador, significa que si existe un objeto de usuario que satisface la expresión de hello proporcionada como valor de hello del parámetro de consulta de filtro de hello, entonces servicio hello es toorespond esperado con un urn: ietf:params:scim:schemas: recursos principales: 2.0:User o urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, incluido solo Hola valor de atributo de Id. de ese recurso.  Hola valo hello **identificador** atributo se conoce toohello solicitante. Se incluye en el valor de Hola Hola filtro del parámetro de consulta; Hola de pidiendo sirve realmente toorequest una representación mínima de un recurso que satisfacen la expresión de filtro de hello como una indicación de si dicho objeto existe.   

  Si el servicio de Hola se compiló mediante bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de Hola se traduce en un método de consulta del proveedor del servicio de hello toohello de llamada. valor de Hola de propiedades de Hola de objeto de hello proporcionado como valor de hello del argumento de parámetros de hello son los siguientes: 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  En este caso, valor Hola de índice Hola x puede ser 0 y valor Hola de Hola y de índice puede ser 1, o valor Hola de x puede ser 1 y valor Hola de y puede ser 0, según el orden de Hola de las expresiones de Hola Hola filtro del parámetro de consulta.   

5. Este es un ejemplo de una solicitud de Azure Active Directory tooan SCIM servicio tooupdate un usuario: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  las bibliotecas de Microsoft Common Language Infrastructure de Hola para implementar servicios SCIM traduciría solicitud Hola un toohello de llamada al método Update del proveedor del servicio de Hola. Aquí es firma Hola de hello método de actualización: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    En el ejemplo de Hola de un usuario de solicitud tooupdate, objeto de hello proporciona como valor de Hola de argumento de revisión de hello tiene estos valores de propiedad: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. un usuario de un almacén de identidades de aprovisionar toode representado por un servicio SCIM, Azure AD envía una solicitud como: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Si el servicio de Hola se compiló mediante bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de Hola se traduce en un método de eliminación del proveedor del servicio de hello toohello de llamada.   Este método tiene esta firma: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  objeto de Hello proporciona como valor de Hola de argumento de hello resourceIdentifier tiene estos valores de propiedad en el ejemplo de Hola de una solicitud toode aprovisionar un usuario: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Aprovisionamiento y cancelación del aprovisionamiento de grupos
Hola siguientes ilustración muestra hello mensajes que Azure AcD envía tooa SCIM servicio toomanage Hola del ciclo de vida de un grupo en otro almacén de identidades.  Los mensajes se diferencian de los mensajes de Hola pertenecen toousers de tres maneras: 

* esquema de Hola de un recurso de grupo se identifica como http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Solicitudes tooretrieve grupos estipulan ese atributo de miembros de hello es toobe excluido de cualquier recurso proporcionado en la solicitud de toohello de respuesta.  
* Las solicitudes toodetermine si un atributo de referencia tiene un valor determinado se trata de solicitudes sobre el atributo de miembros de Hola.  

![][5]
*Figura 6: secuencia de aprovisionamiento y cancelación del aprovisionamiento de grupos*

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Automatizar aplicaciones del usuario aprovisionamiento o desaprovisionamiento tooSaaS](active-directory-saas-app-provisioning.md)
* [Personalización de asignaciones de atributos para el aprovisionamiento de usuarios](active-directory-saas-customizing-attribute-mappings.md)
* [Escritura de expresiones para asignaciones de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de ámbito para el aprovisionamiento de usuario](active-directory-saas-scoping-filters.md)
* [Notificaciones de aprovisionamiento de cuentas](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
