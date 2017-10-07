---
title: "aaaAzure Service Fabric invertir una comunicación segura proxy | Documentos de Microsoft"
description: "Configurar la comunicación segura de extremo a extremo de proxy inverso tooenable."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Conectar el servicio seguro tooa con proxy inverso Hola

Este artículo explica cómo tooestablish conexión segura entre proxy inverso de Hola y servicios, lo que permite un canal seguro de tooend final.

Conectar servicios toosecure se admite solo una vez proxy inverso toolisten configurado en HTTPS. Resto del documento de Hola se da por supuesto que éste es el caso de hello.
Consulte demasiado[proxy en Azure Service Fabric inverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) proxy inverso de hello tooconfigure en Service Fabric.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Establecimiento de conexión segura entre el proxy inverso de Hola y servicios 

### <a name="reverse-proxy-authenticating-tooservices"></a>Invertir tooservices de autenticación de proxy:
Hello proxy inverso identifica a sí mismo tooservices usando su certificado, especificada con ***reverseProxyCertificate*** propiedad Hola **clúster** [sección de tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md). Los servicios pueden implementar Hola lógica tooverify Hola certificado de proxy inverso de Hola. Servicios de Hello pueden especificar detalles del certificado de cliente de hello aceptado como valores de configuración en el paquete de configuración de Hola. Esto se puede leer en tiempo de ejecución y usó toovalidate Hola certificado presentado por el proxy inverso Hola. Consulte demasiado[administrar parámetros de la aplicación](service-fabric-manage-multiple-environment-app-configuration.md) valores de configuración de tooadd Hola. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Invertir la verificación de identidad del servicio de hello mediante certificado Hola presentado por el servicio de Hola de proxy:
tooperform validación de certificados de servidor de certificados de hello presentado por servicios de hello, proxy inverso es compatible con una de las siguientes opciones de hello: ninguno, ServiceCommonNameAndIssuer y ServiceCertificateThumbprints.
tooselect una de estas tres opciones, especifique hello **ApplicationCertificateValidationPolicy** de sección de parámetros de Hola de elemento de ApplicationGateway/Http bajo [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

Consulte toohello siguiente sección para obtener más información sobre la configuración adicional para cada una de estas opciones.

### <a name="service-certificate-validation-options"></a>Opciones de validación de certificados de servicio 

- **Ninguno**: proxy inverso omite la comprobación del certificado de proxy de servicio de Hola y establece la conexión segura de Hola. Se trata del comportamiento predeterminado de Hola.
Especificar hello **ApplicationCertificateValidationPolicy** con valor **ninguno** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.

- **ServiceCommonNameAndIssuer**: proxy inverso comprueba el certificado de hello presentado por servicio de hello en función de nombre común del certificado y la huella digital del emisor inmediato: especificar hello **ApplicationCertificateValidationPolicy**  con valor **ServiceCommonNameAndIssuer** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

lista de hello toospecify de nombre común de servicio y las huellas digitales de emisor, agregue un **ApplicationGateway/Http/ServiceCommonNameAndIssuer** elemento bajo fabricSettings, tal y como se muestra a continuación. En el elemento de matriz de parámetros de hello, pueden agregarse varios pares de huella digital de emisor y nombre común del certificado. 

Si está conectando proxy inverso de punto de conexión de hello toopresents un certificado que es común huella digital del emisor y el nombre coincide con alguno de los valores de hello especificados aquí, se establece el canal SSL. En detalles del error toomatch Hola certificado, proxy inverso produce un error de solicitud del cliente de hello con un código de estado 502 (puerta de enlace incorrecta). Hola línea de estado HTTP también contendrá frase Hola "Certificado SSL no válido". 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: proxy inverso comprobará el certificado del servicio proxy de hello en función de su huella digital. Puede elegir a toogo esta ruta cuando Hola servicios se configuran con certificados autofirmados: especificar hello **ApplicationCertificateValidationPolicy** con valor **ServiceCertificateThumbprints**en la sección de parámetros de hello del elemento de ApplicationGateway/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Especificar huellas digitales de hello con un **ServiceCertificateThumbprints** entrada en la sección de parámetros del elemento de ApplicationGateway/Http. Huellas digitales varios pueden especificarse como una lista separada por comas en el campo de valor de hello, tal y como se muestra a continuación:

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Si Hola huella del certificado de servidor hello aparece en esta entrada de configuración, proxy inverso éxito conexión de SSL de Hola. En caso contrario, termina la conexión de Hola y se produce un error Hola solicitud del cliente con un 502 (puerta de enlace incorrecta). Hola línea de estado HTTP también contendrá frase Hola "Certificado SSL no válido".

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Lógica de selección de punto de conexión cuando los servicios exponen tanto puntos de conexión seguros como no seguros
Service Fabric admite la configuración de varios puntos de conexión para un servicio. Consulte [Especificación de los recursos en un manifiesto de servicio](service-fabric-service-manifest-resources.md).

Proxy inverso selecciona uno de hello extremos tooforward Hola solicitud en función de hello **ListenerName** parámetro de consulta. Si no se especifica, se puede elegir cualquier punto de conexión de lista de puntos de conexión de Hola. Ahora puede ser un punto de conexión HTTP o HTTPS. Puede haber escenarios o requisitos en la que desea toooperate de proxy inverso de hello en un "único modo seguro", es decir no desea Hola segura proxy inverso tooforward solicitudes toounsecured los puntos de conexión. Esto puede lograrse mediante la especificación de hello **SecureOnlyMode** entrada de configuración con el valor **true** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> Cuando se trabaja en **SecureOnlyMode**, si el cliente ha especificado un **ListenerName** correspondiente punto de conexión de tooan HTTP(unsecured), proxy inverso produce un error en solicitud de hello con un código de estado 404 de HTTP (no encontrado).

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Configurar la autenticación de certificado de cliente a través de proxy inverso de Hola
Terminación SSL se produce en el proxy inverso de Hola y se pierden todos los datos del certificado de cliente de Hola. Para la autenticación de certificado de cliente de hello servicios tooperform, establecer hello **ForwardClientCertificate** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.

1. Cuando **ForwardClientCertificate** se establece demasiado**false**, invertir la dirección proxy no se solicitará certificado de cliente de Hola durante su protocolo de enlace SSL con cliente de Hola.
Se trata del comportamiento predeterminado de Hola.

2. Cuando **ForwardClientCertificate** se establece demasiado**true**, invertir las solicitudes de proxy para el certificado del cliente de Hola durante su protocolo de enlace SSL con cliente de Hola.
A continuación, reenvía cliente hello datos del certificado en un encabezado HTTP personalizado denominado **certificado de cliente X**. el valor del encabezado de Hello es la cadena de formato PEM Hola con codificación base64 del certificado del cliente de Hola. servicio Hola puede correctamente o no superado solicitud Hola con código de estado adecuado después de inspeccionar los datos del certificado Hola.
Si el cliente de hello no presenta un certificado, proxy inverso reenvía un encabezado vacío y deje que caso de hello servicio identificador hello.

> El proxy inverso es un simple reenviador. No llevará a cabo ninguna validación de certificado del cliente de Hola.


## <a name="next-steps"></a>Pasos siguientes
* Consulte demasiado[configurar los servicios de proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) ejemplos de plantilla para el Administrador de recursos de Azure tooconfigure proxy inverso seguro con opciones de validación de certificados de servicio diferente de Hola.
* Vea un ejemplo de comunicación HTTP entre los servicios de un [proyecto de ejemplo en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Llamadas a procedimiento remoto con la comunicación remota de Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API web que usa OWIN en Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Administración de certificados del clúster](service-fabric-cluster-security-update-certs-azure.md)
