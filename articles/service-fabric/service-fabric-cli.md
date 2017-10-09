---
title: aaaGet a trabajar con Azure Service Fabric CLI (sfctl)
description: "Obtenga información acerca de cómo toouse Hola CLI de tejido de servicio de Azure. Obtenga información acerca de cómo tooconnect tooa clúster y cómo las aplicaciones de toomanage."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a>Línea de comandos de Azure Service Fabric

Hello Azure Service Fabric CLI (sfctl) es una utilidad de línea de comandos para interactuar y administrar entidades de Azure Service Fabric. Sfctl puede utilizarse con clústeres de Windows o Linux. Sfctl se ejecuta en cualquier plataforma que sea compatible con Python.

## <a name="prerequisites"></a>Requisitos previos

Tooinstallation anterior, asegúrese de que el entorno tiene python y pip instalado. Para obtener más información, eche un vistazo a hello [pip documentación de inicio rápido](https://pip.pypa.io/en/latest/quickstart/)y oficial [python instala documentación](https://wiki.python.org/moin/BeginnersGuide/Download).

Aunque se admite ambos python 2.7 y 3.6, se recomienda toouse python 3.6.

## <a name="install"></a>Instalación

Hello Azure Service Fabric CLI (sfctl) se empaqueta como un paquete de python. tooinstall Hola versión más reciente ejecutar:

```bash
pip install sfctl
```

Después de la instalación, ejecute `sfctl -h` tooget información acerca de los comandos disponibles.

## <a name="cli-syntax"></a>Sintaxis de la CLI

Los comandos siempre tienen el prefijo `sfctl`. Para obtener información general de todos los comandos que puede usar, use `sfctl -h`. Para obtener ayuda con un único comando, use `sfctl <command> -h`.

Seguimiento de comandos una estructura repetible, con destino Hola Hola de comandos anterior verbo de Hola o acción:

```azurecli
sfctl <object> <action>
```

En este ejemplo, `<object>` es destino de Hola para `<action>`.

## <a name="select-a-cluster"></a>Selección de un clúster

Antes de realizar cualquier operación, debe seleccionar una tooconnect de clúster a. Por ejemplo, ejecute hello después tooselect y conectar toohello clúster con el nombre de hello `testcluster.com`.

> [!WARNING]
> No utilice clústeres de Service Fabric que no sean seguros en entornos de producción.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

punto de conexión de clúster de Hello debe ir precedido por `http` o `https`. Debe incluir el puerto de Hola para puerta de enlace de hello HTTP. dirección y el puerto de Hola se Hola igual que la dirección URL del explorador de Service Fabric de Hola.

Para clústeres que están protegidos con un certificado, puede especificar un certificado PEM codificado. certificado de Hello puede especificarse como un único archivo o el certificado y el par de claves.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Para obtener más información, consulte [clúster de Azure Service Fabric segura de conectar tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Operaciones básicas

La información de la conexión del clúster se mantiene en varias sesiones de sfctl. Después de seleccionar un clúster de Service Fabric, puede ejecutar cualquier comando de Service Fabric en clúster de Hola.

Por ejemplo, hello tooget estado de mantenimiento del clúster de Service Fabric, utilice Hola siguiente comando:

```azurecli
sfctl cluster health
```

resultados del comando Hola Hola después de salida:

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

Sugerencias y consejos para resolver problemas comunes.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Convertir un certificado desde el formato de tooPEM PFX

Hola Service Fabric CLI admite certificados de cliente como archivos PEM (extensión .pem). Si utiliza los archivos PFX de Windows, debe convertir esos formato tooPEM de certificados. tooconvert un archivo PEM tooa del archivo PFX, utilice el siguiente comando:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Para obtener más información, vea hello [OpenSSL documentación](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemas de conexión

Algunas operaciones pueden generar Hola siguiente mensaje:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Compruebe que Hola especificado de punto de conexión de clúster está disponible y realizando escuchas. Además, compruebe que Hola que está disponible en la interfaz de usuario del explorador de tejido de servicio de host y puerto. punto de conexión de tooupdate hello, use `sfctl cluster select`.

### <a name="detailed-logs"></a>Registros detallados

Los registros detallados a menudo son útiles al depurar o notificar problemas. Hay un global `--debug` marca que aumenta el nivel de detalle de Hola de archivos de registro.

### <a name="command-help-and-syntax"></a>Ayuda y sintaxis de los comandos

Para obtener ayuda con un comando específico o un grupo de comandos, usar hello `-h` marca:

```azurecli
sfctl application -h
```

Otro ejemplo:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Pasos siguientes

* [Implementar una aplicación con hello Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md)
* [Introducción a Service Fabric con Linux](service-fabric-get-started-linux.md)
