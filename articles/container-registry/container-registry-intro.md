---
title: registros de contenedor de Docker aaaPrivate en Azure | Documentos de Microsoft
description: "Introducción toohello servicio de registro de contenedor de Azure, que proporciona en la nube, administran, registros de Docker privados."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Registros de contenedor de Docker de tooprivate de introducción


Registro de contenedor de Azure es un servicio de [registro de Docker](https://docs.docker.com/registry/) servicio basado en Hola 2.0 de registro de Docker de código abierto. Crear y mantener toostore de registros de contenedor de Azure y administrar su privada [contenedor Docker](https://www.docker.com/what-docker) imágenes. Usar registros de contenedor en Azure con el desarrollo de contenedor existente y las canalizaciones de implementación y dibujar en el cuerpo de Hola de especialización de la Comunidad de Docker.

Para más información sobre Docker y los contenedores, consulte:

* [Guía del usuario de Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Casos de uso
Extraer imágenes de un contenedor de Azure destinos de implementación de toovarious del registro:

* **Sistemas escalables de orquestación** que administran aplicaciones en contenedores a través de clústeres de hosts, incluidos [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) y [Kubernetes](http://kubernetes.io/docs/).
* **Servicios de Azure** que admiten la creación y ejecución de aplicaciones a escala, entre los que se incluyen [Container Service](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) y otros más.

Los desarrolladores también pueden insertar tooa del registro de contenedor como parte de un flujo de trabajo de desarrollo de contenedor. Por ejemplo, puede dirigir un registro de contenedor desde una herramienta de desarrollo e integración continua como [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) o [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Conceptos clave
* **Registro**: cree un registro de contenedor o varios en la suscripción de Azure. Cada registro está respaldado por un estándar Azure [cuenta de almacenamiento](../storage/common/storage-introduction.md) Hola misma ubicación. Aprovechar las ventajas del almacenamiento local, red y cierre de las imágenes de contenedor mediante la creación de un registro de hello misma ubicación de Azure como las implementaciones. Un nombre completo del registro tiene formato de hello `myregistry.azurecr.io`.

  Se [controlar el acceso](container-registry-authentication.md) tooa registro de contenedor mediante una copia de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md) o una cuenta de administrador proporcionado. Ejecución Hola estándar `docker login` tooauthenticate de comando con un registro.

* **Registro administrado**: un nivel que ofrece funcionalidades adicionales para los registros en tres SKU: Basic, Standard y Premium. imágenes de Hello en estos SKU se almacenan en las cuentas de almacenamiento administrado por servicio de los registros de contenedor de Azure, que mejora la fiabilidad y permite ofrecer nuevas características de Hola. Entre las nuevas funcionalidades se incluyen la integración de webhooks, la autenticación del repositorio con Azure Active Directory y la compatibilidad con la funcionalidad de eliminación. Los usuarios tienen Hola opción toochoose entre registros administrados o toocreate respaldado por sus propias cuentas de almacenamiento al crear registros en un registro.

* **Repositorio**: un registro contiene uno o varios repositorios, que son grupos de imágenes de contenedor. Azure Container Registry es compatible con los espacios de nombres del repositorio de varios niveles. Esta característica permite toogroup las colecciones de aplicación específico de imágenes tooa relacionados o una colección de desarrollo de aplicaciones toospecific o los equipos operativos. Por ejemplo:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` representa una imagen de toda la organización
  * `myregistry.azurecr.io/warrantydept/dotnet-build`Representa una imagen utiliza aplicaciones de .NET toobuild, compartidas el departamento de garantía de Hola
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`Representa una imagen de web, agrupada en la aplicación de envíos de cliente de hello, pertenecen al departamento de garantía de Hola

* **Imagen**: se almacena en un repositorio, cada imagen es una instantánea de solo lectura de un contenedor Docker. Los registros de contenedor de Azure pueden incluir imágenes de Windows y de Linux. Controle los nombres de imagen de todas las implementaciones de contenedor. Estándar de uso [comandos Docker](https://docs.docker.com/engine/reference/commandline/) toopush imágenes en un repositorio o una imagen desde un repositorio de extracción.

* **Contenedor**: un contenedor define una aplicación de software y las dependencias ajustadas en un sistema de archivos completo que incluye el código, el tiempo de ejecución, las herramientas del sistema y las bibliotecas. Ejecute contenedores Docker basados en imágenes de Windows o Linux que extrae de un registro de contenedor. Contenedores que se ejecutan en un solo equipo comparten kernel del sistema operativo Hola. Contenedores de docker son totalmente portables tooall principales distribuciones de Linux, Mac y Windows.




## <a name="next-steps"></a>Pasos siguientes
* [Crear un registro de contenedor mediante Hola portal de Azure](container-registry-get-started-portal.md)
* [Crear un registro de contenedor mediante Hola CLI de Azure](container-registry-get-started-azure-cli.md)
* [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md)
* toobuild una integración continua y flujo de trabajo de implementación mediante Visual Studio Team Services, el servicio de contenedor de Azure y registro de contenedor de Azure, vea [este tutorial](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Si desea tooset su propio registro privada de Docker en Azure (sin un punto de conexión público), consulte [implementar su propia privada Docker registro en Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
