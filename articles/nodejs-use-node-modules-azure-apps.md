---
title: "aaaWorking con módulos de Node.js"
description: "Obtenga información acerca de cómo toowork con módulos de Node.js cuando se utiliza el servicio de aplicación de Azure o servicios en la nube."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Uso de módulos Node.js con aplicaciones de Azure
Este documento le proporciona orientación sobre el uso de módulos Node.js con aplicaciones hospedadas en Azure. Mediante este documento podrá asegurarse de que su aplicación usa una versión específica del módulo y de que usa módulos nativos con Azure.

Si ya está familiarizado con el uso de módulos de Node.js, **package.json** y **shrinkwrap.json npm** archivos, Hola siguiente información proporciona un resumen rápido de lo que se describe en este artículo:

* Azure App Service entiende los archivos **package.json** y **npm-shrinkwrap.json** y puede instalar módulos basados en las entradas de estos archivos.

* Los servicios de nube Azure esperan que todos los toobe de módulos instalados en el entorno de desarrollo de Hola y Hola **nodo\_módulos** toobe de directorio incluido como parte del paquete de implementación de Hola. Es posible tooenable soporte para la instalación de los módulos con **package.json** o **shrinkwrap.json npm** archivos en servicios en la nube; sin embargo, esta configuración requiere personalización predeterminado Hola secuencias de comandos utilizadas por los proyectos de servicio en la nube. Para obtener un ejemplo de cómo tooconfigure este entorno, consulte [Azure inicio tarea toorun npm instalar tooavoid implementar módulos de nodo](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Máquinas virtuales de Azure no se tratan en este artículo, como la experiencia de implementación de hello en una máquina virtual depende del sistema de operativo Hola hospedado por hello Máquina Virtual.
> 
> 

## <a name="nodejs-modules"></a>Módulos Node.js
Los módulos son paquetes JavaScript que pueden cargarse y que proporcionan una funcionalidad específica para su aplicación. Módulos normalmente se instalan con hello **npm** de línea de comandos de herramientas, sin embargo algunos módulos (por ejemplo, el módulo http del Hola) se proporcionan como parte del paquete de hello core Node.js.

Cuando se instalan módulos, se almacenan en hello **nodo\_módulos** directorio raíz de hello de la estructura de directorios de la aplicación. Cada módulo en hello **nodo\_módulos** directory mantiene su propio **nodo\_módulos** directorio que contiene los módulos que depende de, y se repite este comportamiento para cada módulo de todas las forma Hola hacia abajo de la cadena de dependencia de Hola. Este entorno permite que cada módulo instalado toohave sus propios requisitos de versión para los módulos de hello depende, sin embargo puede producir una gran estructura de directorio de gran tamaño.

Hola implementación **nodo\_módulos** directorio como parte de la aplicación aumenta el tamaño de Hola de implementación de hello cuando se comparan toousing una **package.json** o  **NPM shrinkwrap.json** archivo; sin embargo, garantiza que las versiones de Hola de módulos de hello usados en producción se Hola igual como módulos de hello usados en el desarrollo de.

### <a name="native-modules"></a>Módulos nativos
Mientras que la mayoría de los módulos son archivos JavaScript sin formato, algunos módulos son imágenes binarias específicas de plataforma. Estos módulos se compilan en el momento de la instalación, normalmente mediante Python y node-gyp. Puesto que los servicios de nube de Azure se basan en hello **nodo\_módulos** carpeta que se implementa como parte de la aplicación hello, cualquier módulo nativo que se incluye como parte de los módulos de hello instalado debería funcionar en un servicio de nube mientras estaba instala y se compila en un sistema de desarrollo de Windows.

Azure App Service no es compatible con todos los módulos nativos y podría presentar errores al compilar módulos con requisitos previos específicos. Aunque algunos módulos conocidos, como MongoDB, tienen dependencias nativas opcionales y funcionan correctamente sin ellas, dos soluciones alternativas han demostrado funcionar correctamente con casi todos los módulos nativos actualmente disponibles:

* Ejecutar **npm instalar** en un equipo de Windows que tenga instalados los requisitos previos de todos los Hola nativo del módulo. A continuación, implemente Hola creado **nodo\_módulos** carpeta como parte de hello aplicación tooAzure servicio de aplicaciones.

  * Antes de compilar, compruebe que la instalación local de Node.js tiene arquitectura coincidente y versión de Hola sea más parecida posible toohello uno utilizados en Azure (se pueden comprobar los valores actuales de hello en tiempo de ejecución de propiedades **process.arch**y **process.version**).

* Servicio de aplicaciones de Azure puede ser intensiva de errores personalizado configurado tooexecute o secuencias de comandos de shell durante la implementación, lo que le otorga Hola comandos personalizados de oportunidad tooexecute y configurar con precisión Hola forma **instalar npm** se está ejecutando. Para un vídeo que se muestra cómo tooconfigure ese entorno, consulte [Scripts de implementación de sitios Web personalizados con Kudu].

### <a name="using-a-packagejson-file"></a>Uso de un archivo package.json
Hola **package.json** archivo es una manera toospecify Hola nivel superior dependencias requiere de la aplicación hello plataforma de hospedaje puede instalar las dependencias de hello, en lugar de requerir hello tooinclude **nodo \_paquetes** carpeta como parte de la implementación de Hola. Una vez implementada la aplicación hello, Hola **npm instalar** comando es hello tooparse usado **package.json** archivo e instalar todas las dependencias de hello enumeradas.

Durante el desarrollo, puede usar hello **--guardar**, **--save-dev**, o **--guardar opcional** parámetros al instalar módulos tooadd una entrada para el módulo de hello tooyour **package.json** archivo automáticamente. Para obtener más información, consulte [npm-install](https://docs.npmjs.com/cli/install).

Un posible problema con hello **package.json** archivo consiste en que especifica solo versión de Hola para las dependencias de nivel superior. Cada módulo instalado puede o no puede especificar la versión de Hola de módulos de hello depende, y por lo que es posible que tenga que terminar con una cadena de dependencia diferentes que Hola uno usados en el desarrollo.

> [!NOTE]
> Al implementar tooAzure servicio de aplicaciones, si su <b>package.json</b> archivo hace referencia a un módulo nativo, es posible que vea un toohello de error similar siguiente ejemplo, al publicar la aplicación hello mediante Git:
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Uso de un archivo npm-shrinkwrap.json
Hola **npm shrinkwrap.json** archivo es un intento de tooaddress Hola módulo limitaciones de las versiones de hello **package.json** archivo. Mientras hello **package.json** archivo sólo incluye versiones de módulos de nivel superior de hello, hello **shrinkwrap.json npm** archivo contiene los requisitos de versión de hello para la cadena de dependencias de módulo completo Hola.

Cuando la aplicación está lista para producción, puede bloquear requisitos de versión y crear un **npm shrinkwrap.json** archivo mediante hello **npm precinto** comando. Este comando usará las versiones de hello instaladas actualmente en hello **nodo\_módulos** carpeta y registra estos toohello versiones **shrinkwrap.json npm** archivo. Después de aplicación hello ha sido implementado toohello entorno de hospedaje, Hola **npm instalar** comando es hello tooparse usado **npm shrinkwrap.json** archivo e instalar todas las dependencias de hello enumeradas. Para más información, consulte [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> Al implementar tooAzure servicio de aplicaciones, si su <b>shrinkwrap.json npm</b> archivo hace referencia a un módulo nativo, es posible que vea un toohello de error similar siguiente ejemplo, al publicar la aplicación hello mediante Git:
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe cómo toouse módulos de Node.js con Azure, obtenga información acerca de cómo demasiado[especificar hello Node.js versión], [compilar e implementar una aplicación web de Node.js](app-service-web/app-service-web-get-started-nodejs.md), y [cómo toouse Hola de línea de comandos de Azure Interfaz para Mac y Linux].

Para obtener más información, vea hello [Centro para desarrolladores de Node.js](/nodejs/azure/).

[especificar hello Node.js versión]: nodejs-specify-node-version-azure-apps.md
[cómo toouse Hola de línea de comandos de Azure Interfaz para Mac y Linux]:cli-install-nodejs.md
[Scripts de implementación de sitios Web personalizados con Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
