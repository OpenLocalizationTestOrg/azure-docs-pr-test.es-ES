---
title: "aaaAzure Service Fabric con inicio rápido de administración de API | Documentos de Microsoft"
description: "Esta guía le mostrará cómo tooquickly comenzar con la administración de API de Azure y el tejido de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Inicio rápido de Service Fabric con Azure API Management

Esta guía le mostrará cómo tooset una copia de seguridad administración de API de Azure con Service Fabric y configurar los primeros servicios de API operación toosend tráfico tooback-end de Service Fabric. toolearn más información acerca de los escenarios de administración de API de Azure con Service Fabric, vea hello [Introducción](service-fabric-api-management-overview.md) artículo. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>Implementar la administración de API y el tejido de servicio tooAzure

Hola primer paso es toodeploy administración de API y un tooAzure de clúster de Service Fabric en una red Virtual compartida. Esto permite toocommunicate de administración de API directamente con el tejido de servicio para que pueda realizar la detección de servicios, resolución de la partición de servicio y reenvíe el tráfico directamente tooany back-end del servicio de Service Fabric.

### <a name="topology"></a>Topología

Esta guía implementa siguiente hello tooAzure topología en la que administración de API y el tejido de servicio están en subredes de Hola misma red Virtual:

 ![Leyenda de la imagen][sf-apim-topology-overview]

tooget a trabajar rápidamente, plantillas de administrador de recursos se proporcionan para cada paso de implementación:

 - Topología de red:
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Clúster de Service Fabric:
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - API Management:
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>Inicie sesión en tooAzure y seleccione su suscripción

En esta guía se usa [Azure PowerShell][azure-powershell]. Cuando se inicia una nueva sesión de PowerShell, inicie sesión en tooyour cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.
 
Inicie sesión en tooyour cuenta de Azure:

```powershell
PS > Login-AzureRmAccount
```

Seleccione su suscripción:

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Cree un grupo de recursos para la implementación. Asígnele un nombre y una ubicación.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Implementar la topología de red de Hola

Hola primer paso es tooset una toowhich de topología de red de hello administración de API y clúster de Service Fabric Hola se va a implementar. Hola [network.json] [ network-arm] plantilla de administrador de recursos es toocreate configurado una red Virtual (VNET) con dos subredes y dos grupos de seguridad de red (NSG). 

Hola [network.parameters.json] [ network-parameters-arm] archivo de parámetros contiene nombres de Hola de subredes de Hola y NSG que se implementará en administración de API y el tejido de servicio. En esta guía, los valores de parámetro hello no es necesario toobe cambiado. plantillas de administración de API y el servicio Administrador de recursos del tejido de Hello utilizan estos valores, por lo que si se modifican aquí, debe modificar otras plantillas de administrador de recursos en hello en consecuencia. 

 1. Descargar Hola siguiente archivo de plantilla y los parámetros del Administrador de recursos:

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. Usar hello siguiendo PowerShell toodeploy Hola Administrador de recursos plantilla y parámetros archivos de comandos para el programa de instalación de red de hello:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Implementar el clúster de Service Fabric Hola

Una vez que han terminado de recursos de red de hello implementar, Hola siguiente paso es toodeploy toohello de clúster de Service Fabric red virtual en la subred de Hola y NSG designado para el clúster de Service Fabric Hola. Para este tutorial, plantilla de servicio Administrador de recursos de tejido de hello es toouse preconfigurada Hola nombres de hello red virtual, subred y NSG que configuró en el paso anterior de Hola. 

plantilla de administrador de recursos de clúster de Service Fabric Hello es toocreate configurado un clúster segura con seguridad de certificado. certificado de Hello es comunicación de nodo a nodo toosecure usado para el clúster y toomanage usuario acceso tooyour Service Fabric. Administración de API usa este Hola de tooaccess servicio de nomenclatura de tejido de servicio de certificado para la detección de servicios.

Este paso requiere un certificado en Key Vault para la seguridad del clúster. Para más información sobre cómo configurar un clúster seguro en Key Vault, consulte [esta guía sobre la creación de un clúster de Azure con Resource Manager](service-fabric-cluster-creation-via-arm.md).

> [!NOTE]
> Autenticación de Azure Active Directory se puede agregar en suma toohello certificado utilizado para el acceso al clúster. Azure Active Directory es hello recomendada clúster Service Fabric de tooyour de acceso de usuario de manera toomanage, pero es toocomplete no es necesario en este tutorial. En cualquier caso, se necesita un certificado para la seguridad de nodo a nodo del clúster y para la autenticación de Azure API Management, que actualmente no admite la autenticación con Azure Active Directory para el back-end de Service Fabric.

 1. Descargar Hola siguiente archivo de plantilla y los parámetros del Administrador de recursos:
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. Rellenar parámetros vacía de hello en hello `cluster.parameters.json` archivo para la implementación, incluyendo hello [información del almacén de claves](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) para el certificado de clúster.

 3. Usar hello después PowerShell comando toodeploy Hola Administrador de recursos plantilla y parámetros archivos toocreate Hola clúster de Service Fabric:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Implementación de API Management

Por último, implementar la administración de API toohello red virtual en la subred de Hola y NSG designado para la administración de API. No es necesario toowait para toofinish de implementación de clúster de Service Fabric Hola antes de implementar la administración de API. 

Para este tutorial, plantilla de administrador de recursos de administración de API de hello es toouse preconfigurada Hola nombres de hello red virtual, subred y NSG que configuró en el paso anterior de Hola. 

 1. Descargar Hola siguiente archivo de plantilla y los parámetros del Administrador de recursos:
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. Rellenar parámetros vacía de hello en hello `apim.parameters.json` para su implementación.

 3. Usar hello siguientes PowerShell comando toodeploy Hola Administrador de recursos plantilla y parámetros archivos para la administración de API:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>Configuración de API Management

Una vez implementados API Management y el clúster de Service Fabric, puede configurar un back-end de Service Fabric en API Management. Esto le permite toocreate una directiva de servicio de back-end que envía el clúster de Service Fabric tooyour de tráfico.

### <a name="api-management-security"></a>Seguridad de API Management

tooconfigure Hola Service Fabric back-end, primero debe tooconfigure configuración de seguridad de administración de API. configuración de seguridad de tooconfigure, vaya a servicio de administración de API tooyour de hello portal de Azure.

#### <a name="enable-hello-api-management-rest-api"></a>Habilitar Hola API de REST de administración

Hola API de REST de administración está actualmente tooconfigure de forma única un servicio back-end de Hola. primer paso de Hello es tooenable hello API de REST de administración y protegerla.

 1. En el servicio de administración de API de hello, seleccione **API de administración - versión preliminar** en **seguridad**.
 2. Comprobar hello **habilitar API de REST de administración de API** casilla de verificación.
 3. Tenga en cuenta Hola URL de la API de administración; éste es dirección URL de hello usaremos tooset posterior de back-end de hello Service Fabric
 4. Generar un **Token de acceso** al seleccionar una fecha de expiración y una clave, a continuación, haga clic en hello **generar** botón hacia la parte inferior de Hola de página de Hola.
 5. Hola copia **token de acceso** y guárdelo: vamos a usar en hello pasos. Tenga en cuenta que esto es diferente de la clave principal de Hola y la clave secundaria.

#### <a name="upload-a-service-fabric-client-certificate"></a>Carga de un certificado de cliente de Service Fabric

Administración de API debe autenticarse con el clúster de Service Fabric para la detección de servicio utilizando un certificado de cliente que tiene acceso tooyour clúster. Por simplicidad, este tutorial se utiliza Hola mismo certificado que se especificó al crear el clúster de Service Fabric hello, que puede ser tooaccess usados de forma predeterminada el clúster.

 1. En el servicio de administración de API de hello, seleccione **certificados de cliente - vista previa** en **seguridad**.
 2. Haga clic en hello **+ agregar** botón
 2. Hola Seleccione archivo de clave privada (.pfx) del certificado de clúster de Hola que especificó al crear el clúster de Service Fabric, asígnele un nombre y proporcionar la contraseña de clave privada de Hola.

> [!NOTE]
> Este tutorial usa Hola mismo certificado para la seguridad de cliente autenticación y clúster de nodo a nodo. Puede utilizar un certificado de cliente independiente si tienes un tooaccess configurado el clúster de Service Fabric.

### <a name="configure-hello-backend"></a>Configurar Hola back-end

Ahora que se configura la seguridad de administración de API, puede configurar el back-end de hello Service Fabric. Para servidores backend de Service Fabric, clúster de Service Fabric hello es Hola back-end, en lugar de un servicio de Service Fabric específico. Esto permite un toomore de tooroute de directiva único que un servicio en clúster de Hola.

Este paso requiere Hola token de acceso que ha generado anteriormente y Hola huella digital para el certificado de clúster que se cargó tooAPI administración en el paso anterior de Hola.

> [!NOTE]
> Si utiliza un certificado de cliente independiente en el paso anterior de hello para la administración de API, deberá huella digital de hello certificado de cliente de hello en suma toohello clúster huella digital del certificado en este paso.

Enviar Hola después toohello de solicitud HTTP PUT URL de la API de administración de API que anotó anteriormente al habilitar el servicio de back-end de hello API de REST de administración tooconfigure Hola Service Fabric. Debería ver un `HTTP 201 Created` en la respuesta al comando Hola se ejecuta correctamente. Para obtener más información sobre cada campo, consulte Administración de API de hello [documentación de referencia de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

Comando HTTP y dirección URL:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

Encabezados de solicitud:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Cuerpo de la solicitud:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Hola **url** parámetro aquí es un nombre de servicio de acceso completa de un servicio en el clúster que todas las solicitudes enruta tooby predeterminado si se especifica ningún nombre de servicio en una directiva de back-end. Puede usar un nombre de servicio falsa, como "fabric: / falsa/servicio" Si no piensa toohave un servicio de reserva.

Consulte administración de API de toohello [documentación de referencia de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) para obtener más detalles sobre cada campo.

#### <a name="example"></a>Ejemplo

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Implementación de un servicio de back-end de Service Fabric

Ahora que tiene Hola que Service Fabric configurado como un tooAPI de back-end administración, puede crear directivas de back-end para las API que envían tráfico tooyour servicios de Service Fabric. Pero primero necesita un servicio que se ejecuta en las solicitudes de tooaccept de Service Fabric.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Creación de un servicio de Service Fabric con un punto de conexión HTTP

Para este tutorial, vamos a crear un básica sin estado ASP.NET confiable servicio principal con plantilla de proyecto de API Web de hello predeterminada. Así se crea un punto de conexión HTTP para el servicio que se expondrá en Azure API Management:

```
/api/values
```

Empiece por [configurar el entorno de desarrollo para ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Una vez configurado el entorno de desarrollo, inicie Visual Studio como administrador y cree un servicio ASP.NET Core:

 1. En Visual Studio, seleccione Archivo -> Nuevo proyecto.
 2. Seleccione la plantilla de aplicación de servicio Fabric hello en la nube y asígnele el nombre **"ApiApplication"**.
 3. Seleccione Hola plantilla de servicio de ASP.NET Core y proyecto de hello name **"WebApiService"**.
 4. Seleccione la plantilla de proyecto de hello Web API de ASP.NET Core 1.1.
 5. Una vez creado el proyecto de hello, abra `PackageRoot\ServiceManifest.xml` y quitar hello `Port` atributo de configuración de recurso del extremo de hello:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Esto permite que un puerto de forma dinámica a partir de intervalo de puertos de aplicación hello, que se abría mediante Hola grupo de seguridad de red en la plantilla de administrador de recursos de clúster de hello, lo que permite el tráfico tooflow tooit de la API de administración de Service Fabric toospecify.
 
 6. Presione F5 en web de Visual Studio tooverify Hola API está disponible localmente. 

    Abra el Explorador de Service Fabric y explorar en profundidad tooa instancia concreta de hello ASP.NET Core toosee Hola dirección base Hola servicio está escuchando en. Agregar `/api/values` toohello dirección base y ábralo en un explorador. Esto invoca el método Get en hello ValuesController en la plantilla de la API Web de Hola Hola. Devuelve respuesta predeterminada de hello proporcionada por la plantilla de hello, una matriz JSON que contiene dos cadenas:

    ```json
    ["value1", "value2"]`
    ```

    Se trata de punto de conexión de Hola que quedará expuesto a través de la API de administración de Azure.

 7. Por último, implementar clústeres de tooyour de aplicación hello en Azure. [Con Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), haga clic en proyecto de aplicación de Hola y seleccione **publicar**. Proporciona el punto de conexión de clúster (por ejemplo, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy Hola aplicación tooyour tejido de servicio de clúster en Azure.

En el clúster de Service Fabric en Azure ahora se ejecutará un servicio sin estado ASP.NET Core denominado `fabric:/ApiApplication/WebApiService`.

## <a name="create-an-api-operation"></a>Creación de una operación de API

Ahora estamos listo toocreate una operación de administración de API que toocommunicate de uso de los clientes externos con Hola servicio sin estado ASP.NET Core se ejecuta en el clúster de Service Fabric Hola.

 1. Inicie sesión en toohello portal de Azure y navegar por la implementación del servicio de administración de API de tooyour.
 2. En la hoja de servicio de administración de API de hello, seleccione **API - vista previa**
 3. Agregar una nueva API haciendo clic en hello **API en blanco** cuadro y rellenar el cuadro de diálogo de hello:

     - **URL de servicio Web**: para los back-end de Service Fabric, no se utiliza. Puede escribir aquí cualquier valor. Para este tutorial usaremos `http://servicefabric`.
     - **Nombre**: proporcione cualquier nombre para la API. Para este tutorial usaremos `Service Fabric App`.
     - **Esquema URL**: seleccione HTTP, HTTPS o ambos. Para este tutorial usaremos `both`.
     - **API URL Suffix** (Sufijo de URL para API): proporcione un sufijo para la API. Para este tutorial usaremos `myapp`.
 
 4. Una vez que se crea Hola API, haga clic en **+ Agregar operación** operación tooadd una API de front-end. Rellene los valores de hello:
    
     - **Dirección URL**: seleccione `GET` y proporcione una ruta de acceso de dirección URL para hello API. Para este tutorial usaremos `/api/values`.
     
       De forma predeterminada, la ruta de acceso de dirección URL de hello especificado aquí se ruta de acceso de dirección URL de hello envía el servicio de Service Fabric toohello back-end. Si usas Hola misma dirección URL aquí que utiliza el servicio, en este caso `/api/values`, a continuación, la operación de hello funciona sin modificaciones adicionales. También puede especificar una ruta de acceso URL aquí que es diferente de la ruta de acceso de dirección URL de hello utilizado por el servicio de Service Fabric, de back-end en cuyo caso tendrá que también toospecify necesidad de volver a escribir una ruta de acceso en la directiva de la operación más tarde.
     - **Nombre para mostrar**: proporcionar un nombre para hello API. Para este tutorial usaremos `Values`.

## <a name="configure-a-backend-policy"></a>Configuración de una directiva de back-end

Directiva de back-end de Hello agrupa todos los componentes. Esto es donde se configura Hola back-end se enrutan las solicitudes de servicio toowhich de Service Fabric. Puede aplicar esta operación de API de tooany de directiva. Hola [configuración de back-end de Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) proporciona controles de enrutamientos de solicitud de siguiente de hello: 
 - Selección de instancia de servicio mediante la especificación de un nombre de instancia de servicio de Service Fabric, ya sea codificado de forma rígida (por ejemplo, `"fabric:/myapp/myservice"`) o generarse a partir de la solicitud de hello HTTP (por ejemplo, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Resolución de la partición mediante la generación de una clave de partición a partir de cualquier esquema de partición de Service Fabric.
 - Selección de réplicas para los servicios con estado.
 - Resolución vuelva a intentar las condiciones que permiten las condiciones de hello toospecify para volver a resolver una ubicación de servicio y volver a enviar una solicitud.

Para este tutorial, cree una directiva de back-end que las rutas de las solicitudes directamente toohello servicio sin estado ASP.NET Core implementó anteriormente:

 1. Seleccionar y editar hello **entrada directivas** para hello `Values` operación haciendo clic en el icono de edición de hello y, a continuación, seleccione **en la vista código**.
 2. En el editor de código de directiva de hello, agregue un `set-backend-service` directiva en las directivas de entrada tal y como se muestra a continuación y haga clic en hello **guardar** botón:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Para obtener un conjunto completo de atributos de directiva de back-end de Service Fabric, consulte toohello [documentación de back-end de administración de API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Agregar Hola API tooa producto. 

Antes de poder llamar a las API de hello, deben agregarse como producto tooa donde puede conceder acceso toousers. 

 1. En el servicio de administración de API de hello, seleccione **productos - vista previa**.
 2. De forma predeterminada, API Management ofrece dos productos: Starter y Unlimited. Seleccione el producto de un número ilimitado de Hola.
 3. Seleccione las API.
 4. Haga clic en hello **+ agregar** botón.
 5. Seleccione hello `Service Fabric App` API que creó en los pasos anteriores de Hola y haga clic en hello **seleccione** botón.

### <a name="test-it"></a>Pruébelo.

Ahora puede intentar enviar un servicio de back-end de solicitud tooyour en Service Fabric a través de la API de administración directamente desde el portal de Azure Hola.

 1. En el servicio de administración de API de hello, seleccione **API - vista previa**.
 2. Hola `Service Fabric App` API que creó en los pasos anteriores de hello, seleccione hello **prueba** ficha.
 3. Haga clic en hello **enviar** botón toosend un servicio de back-end de toohello de solicitud de prueba.

## <a name="next-steps"></a>Pasos siguientes

Llegados a este punto, debe tener una configuración básica de Service Fabric y API Management.

Este tutorial utiliza la autenticación de usuario básica basada en certificados para su tooget de clúster de Service Fabric que preparar rápidamente. aunque para el clúster de Service Fabric es preferible una autenticación de usuarios más avanzada con [autenticación de Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Después, [crear y configurar opciones de producto avanzadas en la administración de API de Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare la aplicación para el tráfico del mundo real.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
