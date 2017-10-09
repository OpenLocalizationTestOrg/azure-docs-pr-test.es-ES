---
title: "aaaDeploy su primer tooCloud de aplicación Foundry en Microsoft Azure | Documentos de Microsoft"
description: "Implementar un tooCloud aplicación Foundry en Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Implementar su primer tooCloud de aplicación Foundry en Microsoft Azure

[Cloud Foundry](http://cloudfoundry.org) es una popular plataforma de aplicaciones de código abierto disponible en Microsoft Azure. En este artículo, le mostramos cómo toodeploy y administrar una aplicación en nube Foundry en un entorno de Azure.

## <a name="create-a-cloud-foundry-environment"></a>Creación de un entorno de Cloud Foundry

Hay varias opciones para crear un entorno de Cloud Foundry en Azure:

- Hola de uso [oferta esencial Foundry nube] [ pcf-azuremarketplace] en hello Azure Marketplace toocreate un entorno estándar que incluye hello Azure Service Broker y PCF Operations Manager. Puede encontrar [completar instrucciones] [ pcf-azuremarketplace-pivotaldocs] para la implementación de marketplace de hello ofrecen Hola documentación esencial.
- Crear un entorno personalizado mediante la [implementación manual de Pivotal Cloud Foundry][pcf-custom].
- [Implementar paquetes de nube Foundry de código abierto de hello directamente] [ oss-cf-bosh] mediante la configuración de un [BOSH](http://bosh.io) director, una máquina virtual que coordina la implementación de hello del entorno de nube Foundry de Hola.

> [!IMPORTANT] 
> Si va a implementar PCF de hello Azure Marketplace, tome nota de hello SYSTEMDOMAINURL y credenciales de administrador de hello necesitan tooaccess Hola esencial el Administrador de aplicaciones, los cuales se describen en la Guía de implementación de marketplace de Hola. Únicamente es necesario toocomplete este tutorial. Para las implementaciones de marketplace, hello SYSTEMDOMAINURL está en hello formulario https://system. *dirección ip*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Conectar toohello controlador de nube

Hola controlador de nube es el entorno de Foundry en la nube de tooa de punto de entrada principal de Hola para implementar y administrar aplicaciones. Hola core API de controlador de nube (CCAPI) es una API de REST, pero es accesible a través de varias herramientas. En este caso, se interactuar con él a través de hello [nube Foundry CLI][cf-cli]. Puede instalar Hola CLI en Linux, Mac OS o Windows, pero si prefiere no tooinstall en absoluto, está disponible preinstalado en hello [Shell en la nube de Azure][cloudshell-docs].

anteponer toolog, `api` toohello SYSTEMDOMAINURL que obtuvo de la implementación de marketplace de Hola. Puesto que la implementación predeterminada de hello usa un certificado autofirmado, también debe incluir hello `skip-ssl-validation` cambiar.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Son toolog solicitada en toohello controlador de nube. Usar credenciales de cuenta de administrador de Hola que adquirió de pasos de implementación de hello marketplace.

En la nube Foundry proporciona *organizaciones* y *espacios* como los equipos de los espacios de nombres tooisolate hello y entornos dentro de una implementación compartida. Hola implementación de marketplace PCF incluye predeterminado hello *system* org y un conjunto de espacios crean toocontain componentes básicos de hello, como servicio de escalado automático de Hola y Hola Azure service broker. Por ahora, elija hello *system* espacio.


## <a name="create-an-org-and-space"></a>Creación de una organización y un espacio

Si escribe `cf apps`, verá un conjunto de aplicaciones de sistema que se han implementado en el espacio de sistema de hello en hello sistema org 

Debe mantener hello *system* org reservado para las aplicaciones del sistema, por lo que crear un toohouse de organización y el espacio de nuestra aplicación de ejemplo.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Use Hola destino comando tooswitch toohello nueva organización y el espacio:

```bash
cf target -o testorg -s dev
```

Ahora, cuando se implementa una aplicación, se crea automáticamente en el espacio y Hola nueva organización. tooconfirm que actualmente no hay ninguna aplicación en hello nuevo org/espacio, escriba `cf apps` nuevo.

> [!NOTE] 
> Para obtener más información acerca de organizaciones y espacios, y cómo se puede usar para el control de acceso basado en roles (RBAC), vea hello [documentación de nube Foundry][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Implementar una aplicación

Vamos a usar una aplicación de nube Foundry de ejemplo denominada Hola Spring en la nube, que está escrito en Java y se basa en hello [Spring Framework](http://spring.io) y [Spring arranque](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Clonar el repositorio de nube de primavera de Hola Hola

Hola aplicación de ejemplo de Hola Spring nube está disponible en GitHub. Clonar tooyour entorno y cambie al directorio nuevo hello:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Compilar la aplicación hello

Aplicación Hola de compilación con [Maven Apache](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Implementar la aplicación hello con inserción cf

Puede implementar la mayoría de las aplicaciones tooCloud Foundry con hello `push` comando:

```bash
cf push
```

Cuando se *inserción* una aplicación, en la nube Foundry detecta el tipo de saludo de la aplicación (en este caso, una aplicación de Java) e identifica sus dependencias (en este caso, Hola Spring marco de trabajo). A continuación, empaqueta todos los elementos requeridos toorun el código en una imagen de contenedor independiente, que se conoce como un *droplet*. Por último, programaciones de nube Foundry Hola aplicación en uno de hello equipos disponibles en su entorno y crea una dirección URL donde se puede llegar a él, que está disponible en la salida de hello de comando de Hola.

![Salida de comando cf push][cf-push-output]

aplicación hello-spring-cloud toosee hello, URL Abrir Hola proporcionado en el explorador:

![Interfaz de usuario predeterminada de Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> toolearn más sobre lo que ocurre durante `cf push`, consulte [cómo se almacenan las aplicaciones] [ cf-push-docs] Hola documentación Foundry en la nube.

## <a name="view-application-logs"></a>Visualización de registros de aplicaciones

Puede usar los registros de tooview de nube Foundry CLI de Hola para una aplicación por su nombre:

```bash
cf logs hello-spring-cloud
```

De forma predeterminada, Hola registra el comando usa *final*, que muestra nuevos registros, tal y como se escriben. aparecen toosee nuevos registros, actualizar la aplicación de nube de primavera de Hola de hello en el Explorador de Hola.

registros de tooview que ya se han escrito, agregar hello `recent` cambiar:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Aplicación Hola a escala

De forma predeterminada, `cf push` solo crea una instancia individual de la aplicación. tooensure alta disponibilidad y escalado habilitar un mayor rendimiento, por lo general desea toorun más de una instancia de las aplicaciones. Puede escalar fácilmente las aplicaciones ya implementadas mediante hello `scale` comando:

```bash
cf scale -i 2 hello-spring-cloud
```

Hola ejecución `cf app` comando en la aplicación hello muestra que en la nube Foundry crea otra instancia de la aplicación hello. Cuando se inicia la aplicación hello, en la nube Foundry inicia automáticamente tooit de tráfico de equilibrio de carga.


## <a name="next-steps"></a>Pasos siguientes

- [Hola de lectura documentación Foundry en la nube][cloudfoundry-docs]
- [Configurar el complemento de Visual Studio Team Services Hola para Foundry en la nube][vsts-plugin]
- [Configurar Hola inyectores de análisis de registro de Microsoft para la nube Foundry][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png