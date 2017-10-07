---
title: aaaGet a trabajar con Azure Service Fabric y 2.0 de CLI de Azure
description: "Obtenga información acerca de cómo toouse hello Azure Service Fabric comandos del módulo de CLI de Azure, versión 2.0. Obtenga información acerca de cómo tooconnect tooa clúster y cómo las aplicaciones de toomanage."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric y CLI de Azure 2.0

Hello Azure herramienta de línea de comandos (CLI de Azure) versión 2.0 incluye toohelp comandos administrar clústeres de Azure Service Fabric. Obtenga información acerca de cómo se inicia tooget con CLI de Azure y el tejido de servicio.

## <a name="install-azure-cli-20"></a>Instalación de la CLI de Azure 2.0

Puede usar toointeract de comandos de CLI de Azure 2.0 con y administrar clústeres de Service Fabric. versión más reciente de hello tooget de CLI de Azure, siga hello [proceso de instalación estándar de CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Para obtener más información, vea hello [información general de CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Sintaxis de la CLI de Azure

Todos los comandos de Service Fabric tienen el prefijo `az sf` en la CLI de Azure. Para obtener información general acerca de los comandos de hello puede utilizar, use `az sf -h`. Para obtener ayuda con un único comando, use `az sf <command> -h`.

Los comandos de Service Fabric en la CLI de Azure siguen este patrón de nomenclatura:

```azurecli
az sf <object> <action>
```

`<object>`es destino de Hola para `<action>`.

## <a name="select-a-cluster"></a>Selección de un clúster

Antes de realizar cualquier operación, debe seleccionar una tooconnect de clúster a. Para obtener un ejemplo, vea Hola siguiente código. código de Hello conecta tooan segura clúster.

> [!WARNING]
> No utilice clústeres de Service Fabric que no sean seguros en entornos de producción.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

punto de conexión de clúster de Hello debe ir precedido por `http` o `https`. Debe incluir el puerto de Hola para puerta de enlace de hello HTTP. dirección y el puerto de Hola se Hola igual que la dirección URL del explorador de Service Fabric de Hola.

Para los clústeres que están protegidos con un certificado, puede usar archivos .pem o .crt y .key sin cifrar. Por ejemplo:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Para obtener más información, consulte [clúster de Azure Service Fabric segura de conectar tooa](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Hola `select` comando no actuar sobre las solicitudes antes de regresar. tooverify que ha especificado un clúster correctamente, utilice un comando como `az sf cluster health`. Compruebe que el comando hello no devuelve los errores.

## <a name="basic-operations"></a>Operaciones básicas

La información de la conexión del clúster se mantiene en varias sesiones de la CLI de Azure. Después de seleccionar un clúster de Service Fabric, puede ejecutar cualquier comando de Service Fabric en clúster de Hola.

Por ejemplo, hello tooget estado de mantenimiento del clúster de Service Fabric, utilice Hola siguiente comando:

```azurecli
az sf cluster health
```

Hola comando genera siguiente de hello resultado (suponiendo que la salida JSON se especifica en configuración de CLI de Azure de hello):

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Sugerencias y solución de problemas

Es posible Hola después información útil si surgen problemas al usar comandos de Service Fabric en CLI de Azure.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Convertir un certificado desde el formato de tooPEM PFX

La CLI de Azure admite los certificados de cliente, como los archivos PEM (extensión .pem). Si utiliza los archivos PFX de Windows, debe convertir esos formato tooPEM de certificados. tooconvert un archivo PEM tooa del archivo PFX, utilice Hola siguiente comando:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Para obtener más información, vea hello [OpenSSL documentación](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemas de conexión

Algunas operaciones pueden generar Hola siguiente mensaje:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Compruebe que Hola especificado de punto de conexión de clúster está disponible y realizando escuchas. Además, compruebe que Hola que está disponible en la interfaz de usuario del explorador de tejido de servicio de host y puerto. punto de conexión de tooupdate hello, use `az sf cluster select`.

### <a name="detailed-logs"></a>Registros detallados

Los registros detallados a menudo son útiles al depurar o notificar problemas. CLI de Azure ofrece global `--debug` marca que aumenta el nivel de detalle de Hola de archivos de registro.

### <a name="command-help-and-syntax"></a>Ayuda y sintaxis de los comandos

Seguimiento de comandos de Service Fabric hello las mismas convenciones que CLI de Azure. Para obtener ayuda con un comando específico o un grupo de comandos, usar hello `-h` marca:

```azurecli
az sf application -h
```

Este es otro ejemplo:

```azurecli
az sf application create -h
```
