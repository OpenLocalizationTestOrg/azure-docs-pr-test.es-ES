---
title: aaaGetting a trabajar con Azure Service Fabric XPlat CLI
description: "Getting started with Azure Service Fabric XPlat CLI (Introducción a la CLI de XPlat de Azure Service Fabric)"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Uso de hello XPlat CLI toointeract con un clúster de Service Fabric

Puede interactuar con el clúster de Service Fabric de máquinas de Linux con hello XPlat CLI en Linux.

primer paso de Hello es obtener última versión de Hola de Hola CLI desde rep de git de Hola y establezca, configúrelo en su ruta de acceso mediante Hola siguientes comandos:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Para cada comando, lo admite, puede escribir nombre de Hola de hello comando tooobtain Hola de ayuda para ese comando.
Se admite la finalización automática para los comandos de Hola. Por ejemplo, hello después proporciona comandos ayuda para todos los comandos de aplicación Hola. 

```sh
 azure servicefabric application 
```

Puede filtrar aún más el comando específico de hello ayuda tooa, como Hola siguiente ejemplo se muestra:

```sh
 azure servicefabric application  create
```

características de Autocompletar tooenable Hola CLI, ejecute hello siguientes comandos:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Hola, siga los comandos conectar toohello clúster y mostrar Hola nodos de clúster de Hola:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse parámetros con nombre y encontrar qué son, puede escribir--ayuda después de un comando. Por ejemplo:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Cuando se conecta el clúster de varios equipos tooa desde un equipo **que no forma parte del clúster de hello**, usar hello siguiente comando:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Reemplace la etiqueta de PublicIPorFQDN de hello con hello real IP o FQDN según corresponda. Cuando se conecta el clúster de varios equipos tooa desde un equipo **que forma parte del clúster de hello**, usar hello siguiente comando:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Puede usar PowerShell o CLI toointeract con el clúster de Service Fabric de Linux creadas a través de hello portal de Azure.

> [!WARNING]
> Estos clústeres no están seguros, por lo tanto, puede abrir su cuadro de uno mediante la adición de la dirección IP pública hello en el manifiesto de clúster de Hola.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Uso de clúster de Service Fabric de XPlat CLI tooconnect tooa Hola

Hola, siga los comandos de CLI de Azure describe cómo tooconnect tooa proteger clústeres. Detalles del certificado Hola deben coincidir con un certificado en nodos de clúster de Hola.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Si el certificado tiene entidades de certificación (CA), deberá tooadd parámetro de ruta de certificado de ca de--hello como el siguiente ejemplo de Hola: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Si tiene varias CA, use una coma como delimitador de Hola.

Si el nombre común de certificado de hello no coincide con el extremo de la conexión de hello, podría utilizar el parámetro hello `--strict-ssl-false` toobypass Hola comprobación tal y como se muestra en el siguiente comando de hello:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Si desea que la comprobación de hello CA tooskip, podría agregar hello: parámetro de false no autorizado rechazar tal y como se muestra en el siguiente comando de hello: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Después de conectarse, debe ser capaz de toorun otro toointeract de comandos CLI con clúster de Hola.

## <a name="deploying-your-service-fabric-application"></a>Implementación de la aplicación de Service Fabric

Ejecute hello siga los comandos toocopy, registrar e iniciar la aplicación de tejido de servicio de hello:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Actualización de la aplicación

proceso de Hello es similar toohello [procesos de Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Compile, copie, registre y cree su aplicación desde el directorio raíz del proyecto. Si la instancia de la aplicación se denomina `fabric:/MySFApp`y es de tipo hello MySFApp, comandos de hello sería como sigue:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Asegúrese de hello tooyour aplicación de cambios y volver a generar servicio Hola modificado.  Hola actualización había modificado archivo de manifiesto del servicio (ServiceManifest.xml) con las versiones de hello actualizado para hello servicio (y código o configuración o datos según corresponda). También modificar el manifiesto de la aplicación hello (ApplicationManifest.xml) con el número de versión de Hola actualizado para aplicación hello y Hola servicio modificado.  Ahora, copiar y registrar la aplicación actualizada con hello siguientes comandos:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Ahora, puede iniciar la actualización de la aplicación hello con hello siguiente comando:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Ahora puede supervisar la actualización de la aplicación hello mediante SFX. En unos minutos, habría actualizó la aplicación hello. También intente una aplicación actualizada con un error y comprobar la funcionalidad de reversión automática de hello en el tejido de servicio.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>Convertir de PFX tooPEM y viceversa.

Tendrá que tooinstall un certificado de los clústeres seguros de tooaccess máquina local (con Windows o Linux) que pueden estar en un entorno diferente. Por ejemplo, al tener acceso a un clúster de Linux seguro desde un equipo Windows y viceversa deberá tooconvert el certificado del PFX tooPEM y viceversa. 

tooconvert desde un archivo PFX de PEM archivo tooa, Hola de uso siguiente comando:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert desde un archivo PEM de tooa del archivo PFX, Hola de uso siguiente comando:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Consulte demasiado[OpenSSL documentación](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) para obtener más información.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Solución de problemas


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Copia del paquete de aplicación hello no se realiza correctamente

Compruebe si `openssh` está instalado. De forma predeterminada, el escritorio Ubuntu no lo tiene instalado. Instalar mediante el siguiente comando de hello:

```sh
sudo apt-get install openssh-server openssh-client**
```

Si persiste el problema de hello, pruebe a deshabilitar PAM para ssh cambiando hello `sshd_config` archivo mediante Hola siguientes comandos:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Si Hola problema todavía persiste, intente creciente número de Hola de ssh sesiones mediante la ejecución de hello siguientes comandos:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Usar claves de ssh autenticación (como toopasswords opuestos) aún no se admite (como plataforma de hello utiliza ssh toocopy paquetes), por lo que utilice autenticación de contraseña en su lugar.

## <a name="next-steps"></a>Pasos siguientes

[Configurar el entorno de desarrollo de hello e implementar un clúster de Service Fabric aplicación tooa Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Artículos relacionados

* [Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Introducción a Service Fabric y la CLI de Azure 2.0)
