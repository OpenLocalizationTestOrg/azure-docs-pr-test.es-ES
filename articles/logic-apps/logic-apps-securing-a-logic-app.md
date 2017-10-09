---
title: "aaaSecure tener acceso a las aplicaciones lógicas tooAzure | Documentos de Microsoft"
description: "Aumenta la seguridad para la protección de acceso tootriggers, entradas y salidas, parámetros de acción y servicios que se utilizan con flujos de trabajo en las aplicaciones lógicas de Azure."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Proteger el acceso a las aplicaciones lógicas tooyour

Hay muchas herramientas toohelp disponibles que proteja la aplicación lógica.

* Protección de acceso tootrigger una aplicación lógica (desencadenador de solicitud de HTTP)
* Protección de acceso toomanage, editar o leer una lógica de aplicación
* Protección de acceso toocontents de entradas y salidas para una ejecución
* Protección de parámetros o entradas en las acciones de un flujo de trabajo
* Protección de acceso tooservices que reciben las solicitudes de un flujo de trabajo

## <a name="secure-access-tootrigger"></a>Acceso seguro tootrigger

Cuando se trabaja con una aplicación de la lógica que se activa en una solicitud HTTP ([solicitar](../connectors/connectors-native-reqres.md) o [Webhook](../connectors/connectors-native-webhook.md)), puede restringir el acceso para que solo los clientes autorizados pueden activar la aplicación de la lógica de hello. Todas las solicitudes en una aplicación lógica se cifrarán y se protegerán mediante SSL.

### <a name="shared-access-signature"></a>Firma de acceso compartido

Cada extremo de la solicitud para una aplicación de lógica incluye un [firma de acceso compartido (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) como parte de la dirección URL de Hola. Cada dirección URL contiene un parámetro de consulta `sp`, `sv` y `sig`. Los permisos se especifican mediante `sp`, y corresponden a los métodos de tooHTTP permitidos, `sv` es toogenerate de la versión utilizada de hello, y `sig` es tooauthenticate usa acceso tootrigger. firma de Hola se genera mediante el algoritmo de hello SHA256 con una clave secreta en todas las rutas de acceso de dirección URL de Hola y propiedades. clave secreta de Hello nunca se exponen y se publica y se mantienen cifrados y almacenados como parte de la aplicación de la lógica de hello. La aplicación lógica sólo autoriza a los desencadenadores que contienen una firma válida creada con la clave secreta de Hola.

#### <a name="regenerate-access-keys"></a>Regenerar las claves de acceso

Puede volver a generar una nueva clave segura en cualquier momento a través del portal de Azure o la API de REST de Hola. Todas las direcciones URL actuales que se generaron anteriormente usando Hola antigua clave son aplicación de lógica de hello toofire invalidado y ya no está autorizado.

1. Hola portal de Azure, abra la aplicación de lógica de hello desea tooregenerate una clave
1. Haga clic en hello **teclas de acceso** elemento de menú en **configuración**
1. Elegir tooregenerate clave hello y proceso de hello completa

Recuperar después de la regeneración de las direcciones URL se firman con la nueva clave de acceso Hola.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Creación de direcciones URL de devolución de llamada con una fecha de expiración

Si va a compartir la dirección URL de hello con otras entidades, puede generar direcciones URL con determinadas claves y fechas de caducidad según sea necesario. Puede, a continuación, perfectamente recorrer las claves, o asegúrese de toofire de acceso a una aplicación está restringido tooa cierto timespan. Puede especificar una fecha de expiración para una dirección URL a través de hello [las aplicaciones lógicas de API de REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

En el cuerpo de hello, incluir propiedad hello `NotAfter` como una cadena de fecha JSON, que devuelve una dirección URL de devolución de llamada que solo es válida hasta hello `NotAfter` fecha y hora.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Creación de direcciones URL con clave secreta principal o secundaria

Cuando se genera o lista de direcciones URL de devolución de llamada para los desencadenadores basados en la solicitud, también puede especificar la dirección URL de toouse clave toosign Hola.  Puede generar una dirección URL firmada por una clave específica a través de hello [las aplicaciones lógicas de API de REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers) como se indica a continuación:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

En el cuerpo de hello, incluir propiedad hello `KeyType` como `Primary` o `Secondary`.  Esto devuelve una dirección URL firmada por la clave segura Hola especificada.

### <a name="restrict-incoming-ip-addresses"></a>Restricción de las direcciones IP entrantes

Además toohello firma de acceso compartido, puede llamar toorestrict llamar a una aplicación lógica solo desde clientes específicos.  Por ejemplo, si administra el punto de conexión a través de administración de API de Azure, puede restringir la lógica de hello tooonly aplicación aceptar la solicitud de hello cuando solicitud de hello provenga de hello dirección IP de instancia de administración de API.

Esta configuración se puede configurar en la configuración de la aplicación hello lógica:

1. Hola portal de Azure, abra la aplicación de lógica de hello desea tooadd restricciones de dirección IP
1. Haga clic en hello **configuración de control de acceso** elemento de menú en **configuración**
1. Especificar lista de Hola de toobe de intervalos de direcciones IP aceptada por el desencadenador de Hola

Un intervalo IP válido toma el formato de hello `192.168.1.1/255`. Si desea que Hola lógica aplicación tooonly incendio como una aplicación de lógica anidadas, seleccione hello **otras aplicaciones de la lógica** opción. Esta opción escribe un recurso de toohello matriz vacía, lo que significa que sólo las llamadas realizadas desde Hola propio servicio incendio (aplicaciones de la lógica principal) correctamente.

> [!NOTE]
> Todavía puede ejecutar una aplicación de lógica con un desencadenador de solicitud a través de la API de REST de Hola / administración `/triggers/{triggerName}/run` independientemente de IP. Este escenario requiere autenticación contra Hola API de REST de Azure, y todos los eventos aparecería en hello registro de auditoría de Azure. Establezca las directivas de control de acceso en consecuencia.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Establecer los intervalos de IP en la definición de recursos de Hola

Si usas un [plantilla de implementación](logic-apps-create-deploy-template.md) tooautomate las implementaciones, la configuración de intervalos IP de hello pueden configurarse en la plantilla de recursos de Hola.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Adición de Azure Active Directory, OAuth u otra seguridad

tooadd autorización más protocolos encima de una aplicación lógica, [administración de API de Azure](https://azure.microsoft.com/services/api-management/) ofrece enriquecido supervisión, seguridad, directivas y documentación para cualquier extremo con hello capacidad tooexpose una aplicación lógica como una API. Administración de API de Azure puede exponer un punto de conexión público o privado para la aplicación de lógica de hello, que puede usar Azure Active Directory, certificado, OAuth u otros estándares de seguridad. Cuando se recibe una solicitud, administración de API de Azure reenvía Hola solicitud toohello lógica aplicación (realizando las transformaciones necesarias o restricciones sobre la marcha). Puede usar el intervalo de IP entrante Hola configuración en tooonly de aplicación lógica de hello permite desencadena toobe de aplicación lógica de hello de la API de administración de.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Proteger el acceso a las aplicaciones lógicas toomanage o editar

Puede restringir las operaciones de toomanagement de acceso en una aplicación de la lógica para que sólo determinados usuarios o grupos estén tooperform capaz de operaciones en recursos de Hola. Las aplicaciones lógicas usan hello Azure [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md) de características y puede personalizarse con hello mismas herramientas.  Hay algunas funciones integradas que puede asignar a los miembros de su suscripción tooas bien:

* **Colaborador de aplicación lógica** -proporciona acceso tooview, editar y actualizar una aplicación de lógica.  No se puede quitar el recurso de Hola o realizar operaciones de administración.
* **Operador de aplicación lógica** : puede ver la aplicación de la lógica de Hola y el historial de ejecución y habilitar o deshabilitar.  No se puede editar o actualizar la definición de Hola.

También puede usar [bloqueo de recurso de Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent cambiar o eliminar aplicaciones lógicas. Esta capacidad es tooprevent valiosos recursos de producción de cambios o eliminaciones.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Acceso seguro toocontents de hello historial de ejecución

Puede restringir el acceso toocontents de entradas o salidas de intervalos de direcciones IP de anterior se ejecuta toospecific.  

Todos los datos dentro de una ejecución de flujo de trabajo se cifran en tránsito y en reposo. Cuando se realiza un historial de toorun de llamada, el servicio de hello autentica la solicitud de Hola y proporciona vínculos toohello solicitud y respuesta entradas y salidas de. Este vínculo puede ser protegidas solicitudes para que solamente tooview contenido de un intervalo de direcciones IP designado devolver el contenido de Hola. Puede utilizar esta funcionalidad para el control de acceso adicional. Incluso puede especificar una dirección IP como `0.0.0.0` para que nadie tenga acceso a las entradas o salidas. Sólo un usuario con permisos de administrador puede quitar esta restricción, proporcionando la posibilidad de Hola para contenido de acceso 'just-in-time' tooworkflow.

Este valor se puede configurar en la configuración de recursos de Hola de hello portal de Azure:

1. Hola portal de Azure, abra la aplicación de lógica de hello desea tooadd restricciones de dirección IP
1. Haga clic en hello **configuración de control de acceso** elemento de menú en **configuración**
1. Especificar lista de Hola de intervalos de direcciones IP para toocontent de acceso

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Establecer los intervalos de IP en la definición de recursos de Hola

Si usas un [plantilla de implementación](logic-apps-create-deploy-template.md) tooautomate las implementaciones, la configuración de intervalos IP de hello pueden configurarse en la plantilla de recursos de Hola.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Parámetros seguros y entradas dentro de un flujo de trabajo

Puede ser conveniente tooparameterize algunos aspectos de una definición de flujo de trabajo para la implementación a través de entornos. Además, algunos parámetros pueden ser parámetros de seguros no desea tooappear al editar un flujo de trabajo, como un identificador de cliente y el secreto del cliente para [autenticación de Azure Active Directory](../connectors/connectors-native-http.md#authentication) de una acción HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Uso de parámetros y parámetros seguros

Hola tooaccess valor de un parámetro de recurso en tiempo de ejecución, hello [lenguaje de definición de flujo de trabajo](http://aka.ms/logicappsdocs) proporciona un `@parameters()` operación. Asimismo, puede [especificar parámetros de plantilla de implementación de recursos de hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Sin embargo, si especifica el tipo de parámetro hello como `securestring`, parámetro hello no se devolverá con rest Hola Hola de definición de recurso y no será accesible mediante la visualización de los recursos de hello después de la implementación.

> [!NOTE]
> Si el parámetro se utiliza en encabezados de Hola o el cuerpo de una solicitud, parámetro hello puede verse obtengan acceso al historial de hello ejecutar y solicitud HTTP de salida. Asegúrese de tooset seguro de las directivas de acceso al contenido en consecuencia.
> Los encabezados de autorización nunca son visibles a través de entradas o salidas. Por lo que si se utiliza el secreto de hello no existe, secreto de hello no está recuperable.

#### <a name="resource-deployment-template-with-secrets"></a>Plantilla de implementación de recursos con secretos

Hello en el ejemplo siguiente se muestra una implementación que hace referencia a un parámetro de secure `secret` en tiempo de ejecución. En un archivo de parámetros separados, puede especificar valor de entorno de Hola para hello `secret`, o use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secretos en tiempo de implementación.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Proteger el acceso a las solicitudes de recepción de tooservices de un flujo de trabajo

Hay segura de que cualquier aplicación de lógica de hello de punto de conexión debe tooaccess toohelp de muchas maneras.

### <a name="using-authentication-on-outbound-requests"></a>Uso de la autenticación en las solicitudes salientes

Cuando se trabaja con un HTTP, HTTP + Swagger (API abierta) o Webhook acción, puede agregar solicitud de toohello de autenticación que se envían. Podría incluir la autenticación básica, la autenticación de certificados o la autenticación de Azure Active Directory. Obtener más información sobre cómo tooconfigure esta autenticación puede encontrarse [en este artículo](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Restringir el acceso toologic aplicación las direcciones IP

Todas las llamadas de las aplicaciones lógicas proceden de un conjunto específico de direcciones IP por región. Puede agregar un filtrado adicional tooonly Aceptar las solicitudes de los designa las direcciones IP. Para obtener una lista de esas direcciones IP, vea [Límites y configuración de Logic Apps](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Conectividad local

Las aplicaciones lógicas proporcionan integración con varios tooprovide de servicios seguras y confiables comunicación local.

#### <a name="on-premises-data-gateway"></a>Puerta de enlace de datos local

Muchos conectores administrados para las aplicaciones lógicas proporcionan una conectividad segura sistemas de tooon locales, como sistema de archivos, SQL, SharePoint, DB2 etc.. puerta de enlace de Hello transmite datos desde orígenes locales en los canales cifrados a través de hello Azure Service Bus. Todo el tráfico se origina como proteger el tráfico saliente desde el agente de puerta de enlace de Hola. Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Administración de API de Azure

[Administración de API de Azure](https://azure.microsoft.com/services/api-management/) tiene opciones de conectividad local, incluida la integración de ExpressRoute y VPN de sitio a sitio para sistemas de tooon locales de proxy y la comunicación seguras. Hola diseñador la lógica de aplicación, puede seleccionar rápidamente una API expuesta de administración de API de Azure dentro de un flujo de trabajo, proporciona acceso rápido sistemas tooon locales.

#### <a name="hybrid-connections-from-azure-app-service"></a>Conexiones híbridas desde Azure App Service

Puede usar características de conexión híbrida de hello locales para la API de Azure y Web aplicaciones toocommunicate en instalaciones locales.  Obtener más información sobre las conexiones híbridas y cómo puede encontrarse tooconfigure [en este artículo](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Pasos siguientes
[Creación de una plantilla de implementación](logic-apps-create-deploy-template.md)  
[Control de excepciones](logic-apps-exception-handling.md)  
[Supervisar las aplicaciones lógicas](logic-apps-monitor-your-logic-apps.md)  
[Diagnóstico de errores y problemas de las aplicaciones lógicas](logic-apps-diagnosing-failures.md)  
