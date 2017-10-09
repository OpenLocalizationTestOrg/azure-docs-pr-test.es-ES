---
title: "aaaAzure aplicación servicio de aplicaciones Web de preguntas más frecuentes de Linux | Documentos de Microsoft"
description: "Este artículo trata sobre las preguntas más frecuentes sobre Web App on Linux de Azure App Service."
keywords: "azure app service, web app, preguntas más frecuentes, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Preguntas más frecuentes sobre Web App on Linux de Azure App Service

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Con la versión de Hola de aplicación Web en Linux, estamos trabajando para agregar características y realizar la plataforma de tooour de mejoras. Aquí son algunas preguntas frecuentes (P+F) que nuestros clientes han estado solicitando a nosotros a través de Hola últimos meses.
Si tiene alguna pregunta, el comentario de artículo de hello y, responderemos tan pronto como sea posible.

## <a name="built-in-images"></a>Imágenes integradas

**P: ¿** quiero toofork hello Docker contenedores integrados que Hola plataforma proporciona. ¿Dónde puedo encontrar esos archivos?

**R.:** Encontrará todos los archivos de Docker en [GitHub](https://github.com/azure-app-service). Puede encontrar todos los contenedores de Docker en [Docker Hub](https://hub.docker.com/u/appsvc/).

**P: ¿** ¿cuáles son valores esperados de Hola para hello sección del archivo de inicio al configurar la pila de tiempo de ejecución de Hola?

**R:** para Node.Js, especifique el archivo de configuración de hello PM2 o el archivo de script. Para .Net Core, debe especificar el nombre del archivo DLL compilado. Para Ruby, puede especificar Hola Ruby script que quiere que tooinitialize su aplicación con.

## <a name="management"></a>Administración

**P: ¿** ¿qué ocurre cuando presione el botón de reinicio de Hola Hola portal de Azure?

**R:** esto es Hola equivalente del reinicio de Docker.

**P: ¿** ¿se puede usar la máquina virtual (VM) del contenedor de aplicación de toohello Shell seguro (SSH), tooconnect?

**R:** Sí, puede hacer que a través del sitio SCM hello, artículo comprobación Hola siguiente para obtener más información [compatibilidad SSH para la aplicación Web en Linux](./app-service-linux-ssh-support.md)

**P: ¿** quiero toocreate un plano Linux App Service enviada mediante SDK o una plantilla de ARM, ¿cómo puedo lograr esto?

**R:** necesita hello tooset `reserved` campo de la aplicación hello servicio demasiado`true`.

## <a name="continuous-integrationdeployment"></a>Integración e implementación continuas

**P: ¿** mi aplicación web sigue usando una imagen de contenedor de Docker antigua después de actualizar la imagen de hello en Docker Hub. ¿Se admite la integración e implementación continuas de contenedores personalizados?

**R:** tooset la implementación/integración continua para las imágenes del registro de contenedor de Azure o DockerHub por Hola de verificación artículo siguiente [implementación continua con la aplicación Web de Azure en Linux](./app-service-linux-ci-cd.md). Para registros privados, puede actualizar el contenedor de hello deteniendo y, a continuación, iniciar la aplicación web. O bien, puede cambiar o agregar una aplicación ficticia establecer tooforce una actualización del contenedor.

**P.**: ¿Los entornos de ensayo son compatibles?

**R:** Sí.

**P: ¿** puedo usar **WebDeploy** toodeploy mi aplicación web?

**R:** Sí, necesita una aplicación llamada tooset `WEBSITE_WEBDEPLOY_USE_SCM` demasiado`false`.

## <a name="language-support"></a>Compatibilidad con idiomas

**P.:** ¿Se admiten aplicaciones de .NET Core sin compilar?

**R:** Sí.

**P.:** ¿Admite un compositor como un administrador de dependencias para aplicaciones PHP?

**R:** Sí. Durante una implementación de Git, Kudu debería detectar que va a implementar una aplicación PHP (gracias toohello presencia de un archivo composer.json) y desencadenará una instalación de compositor automáticamente.

## <a name="custom-containers"></a>Contenedores personalizados

**P.:** Utilizo mi propio contenedor personalizado. Mi aplicación reside en hello `\home\` directorio, pero no podemos encontrar Mis archivos al examinar el contenido de hello mediante el uso de hello [sitio SCM](https://github.com/projectkudu/kudu) o un cliente FTP. ¿Dónde están mis archivos?

**R:** montamos un toohello del recurso compartido SMB `\home\` directory. Esto invalida cualquier contenido de dicho directorio.

**P.:** Utilizo mi propio contenedor personalizado. No deseo Hola plataforma toomount un toohello de recurso compartido SMB `\home\`.

**R:** para hacer que debe establecer hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicación establecer demasiado`false`.

**P: ¿** mi contenedor personalizado toma un toostart mucho tiempo y finalice de contenedor de Hola de reinicio de hello plataforma antes de que iniciarse.

**R:** puede configurar tiempo de hello plataforma Hola esperará antes de reiniciar el contenedor. Esto puede hacerse por establecer hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello de configuración de aplicación el valor deseado en segundos. valor predeterminado de Hello es 230 segundos y Hola max es 600 segundos.

**P: ¿** ¿qué es el formato de hello para la dirección url del servidor de registro privada?

**R:** que debe tooprovide Hola completo registro dirección url como `http://` o `https://`.

**P: ¿** ¿qué es el formato de hello para el nombre de la imagen de hello en la opción de registro privada?

**R:** necesita nombre de la imagen completa de hello tooadd incluida (p. ej dirección url de registro privada de Hola. myacr.azurecr.io/dotnet:latest)

**P: ¿** deseo tooexpose más de un puerto en mi imagen de contenedor personalizadas. ¿Es posible?

**R.:** Actualmente no se admite.

**P:** ¿Puedo traer mi propio almacenamiento?

**R.:** Actualmente no se admite.

**P: ¿** no se puede examinar los procesos de sistema o de ejecución de archivos de mi contenedor personalizado desde el sitio SCM Hola. ¿Por qué ocurre esto?

**R:** sitio SCM Hola se ejecuta en un contenedor independiente. No se pueden comprobar sistema de archivos de Hola o procesos de contenedor de la aplicación hello en ejecución.

**P: ¿** mi contenedor personalizado escucha tooa puerto distinto al puerto 80. ¿Cómo puedo configurar mi puerto aplicación tooroute Hola solicitudes toothat?

**R:** contamos con detección automática del puerto, también puede especificar una aplicación llamada **WEBSITES_PORT**y asígnele el valor de Hola Hola esperada número de puerto. Anteriormente utilizaba plataforma hello `PORT` aplicación establecer, se está planeando toodeprecate Hola use esta configuración de aplicación y mover toousing `WEBSITES_PORT` exclusivamente.

**P: ¿** es necesario tooimplement HTTPS en mi contenedor personalizadas.

**R:** No, plataforma Hola controla la terminación HTTPS en hello compartido front-ends.

## <a name="pricing-and-sla"></a>Precios y contrato de nivel de servicio

**P: ¿** ¿qué es Hola precios mientras utiliza la versión preliminar pública de hello?

**R:** se le cobrará la mitad el número de Hola de horas que se ejecuta la aplicación, con hello precios normal del servicio de aplicación de Azure. Esto significa que hay un descuento del 50 por ciento en los precios normales de Azure App Service.

## <a name="other"></a>Otros

**P: ¿** ¿qué son Hola admitida caracteres en nombres de configuración de aplicación?

**R:** solo puede usar A-z, a-z, 0-9 y Hola guión bajo Configuración de la aplicación.

**P:**  ¿Dónde puedo solicitar nuevas características?

**R:** puede enviar su idea en hello [foro de comentarios de las aplicaciones Web](https://aka.ms/webapps-uservoice). Agregar un título de toohello "[Linux]" de su idea.

## <a name="next-steps"></a>Pasos siguientes
* [¿Qué es Web App on Linux de Azure?](app-service-linux-intro.md)
* [Compatibilidad con SSH para Web App on Linux de Azure](./app-service-linux-ssh-support.md)
* [Configuración de entornos de ensayo en Azure App Service](./web-sites-staged-publishing.md)
* [Implementación continua con Azure Web App en Linux](./app-service-linux-ci-cd.md)
