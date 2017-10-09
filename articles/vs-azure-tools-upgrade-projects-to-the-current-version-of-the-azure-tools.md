---
title: "aaaHow tooupgrade proyectos toohello versión actual de Hola herramientas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupgrade un Azure proyecto en la versión actual de Visual Studio toohello de hello herramientas de Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>¿Cómo tooupgrade proyectos toohello versión actual de hello Azure Tools para Visual Studio
## <a name="overview"></a>Información general
Después de instalar la versión actual de Hola de hello Azure Tools (o una versión anterior más reciente que 1.6), todos los proyectos que se crearon con una herramienta de Azure Tools antes de la versión 1.6 (noviembre de 2011) se actualizarán automáticamente en cuanto se abran. Si crea proyectos mediante Hola versión de 1.6 (noviembre de 2011) de las herramientas y sigue teniendo esa versión instalada, puede abrir esos proyectos en la versión anterior de Hola y decidir más tarde si tooupgrade ellos.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Cómo cambia un proyecto al actualizarlo
Si un proyecto se actualiza automáticamente o especificar que desea tooupgrade, el proyecto es modifica toowork con las versiones actuales de determinados ensamblados, y también se modifican algunas propiedades tal como se describe en esta sección. Si su proyecto requiere otro toobe cambios compatible con la versión más reciente de Hola de herramientas de hello, debe realizar los cambios manualmente.

* archivo web.config de Hello para los roles web y archivo app.config de hello para roles de trabajo son de la versión más reciente de tooreference actualizada Hola de Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* los ensamblados Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll y Microsoft.WindowsAzure.ServiceRuntime.dll Hola son toohello actualizado nuevas versiones.
* Perfiles de publicación que se almacenaron en el archivo de proyecto de Azure (.ccproj) de hello son tooa ha movido los archivo independiente, con hello extensión .azurePubXml, en hello **publicar** subdirectorio.
* Perfil de publicación de algunas propiedades en hello está actualizado toosupport características nuevas y modificadas. **AllowUpgrade** se reemplaza por **DeploymentReplacementMethod**, ya que los servicios en la nube implementados se pueden actualizar de forma simultánea o incremental.
* Hola propiedad **UseIISExpressByDefault** se agrega y establecer toofalse de modo que hello servidor web que se utiliza para la depuración no cambie automáticamente de Internet Information Services (IIS) tooIIS Express. IIS Express es el servidor de web de hello predeterminado para los proyectos creados con versiones más recientes de Hola de herramientas de Hola.
* Si el almacenamiento en caché de Azure se hospeda en uno o varios roles del proyecto, se modifican algunas propiedades de configuración de servicio de hello (archivo .cscfg) y la definición de servicio (archivo .csdef) cuando se actualiza un proyecto. Si el proyecto de hello usa paquetes de NuGet de almacenamiento en caché de Azure de hello, proyecto de hello es toohello actualizado la versión más reciente del paquete de saludo. Debe abrir el archivo web.config de hello y compruebe que configuración de cliente de Hola se mantiene correctamente durante el proceso de actualización de Hola. Si agrega ensamblados de cliente de almacenamiento en caché de hello referencias tooAzure sin usar el paquete de NuGet hello, estos ensamblados no se actualizarán; debe actualizar manualmente estas referencias toohello las nuevas versiones.

> [!IMPORTANT]
> Para proyectos de F #, debe actualizar manualmente los ensamblados de tooAzure de referencias para que hagan referencia a versiones más recientes de Hola de esos ensamblados.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>¿Cómo tooupgrade un Azure proyecto versión actual de toohello
1. Instalación Hola versión actual de hello Azure Tools en la instalación de Hola de Visual Studio que quiere toouse de Hola Actualizar proyecto y proyecto de hello, a continuación, abra que desea tooupgrade. Si el proyecto de Hola se creó con un Azure Tools versión 1.6 (noviembre de 2011), proyecto de hello es la versión actual de toohello actualizado automáticamente. Si se creó el proyecto de hello con hello versión de noviembre de 2011 y todavía está instalada la versión, abre el proyecto hello en esa versión.
2. En el Explorador de soluciones, menú contextual de hello abierta para el nodo del proyecto hello, elija **propiedades**y, a continuación, elija hello **aplicación** ficha Hola del cuadro de diálogo que aparece.
   
    Hola **aplicación** pestaña muestra la versión de herramientas de Hola que está asociado con el proyecto de Hola. Si aparece la versión actual de Hola de Azure Tools, proyecto de hello ya se ha actualizado. Si ha instalado una versión más reciente de las herramientas de Hola que se muestra en la pestaña de hello, un **actualizar** aparece el botón.
3. Elija hello **actualizar** botón tooupgrade una versión actual del proyecto toohello de herramientas de Hola.
4. Compile el proyecto de hello y, a continuación, solucione los errores resultantes de los cambios en la API. Para obtener información acerca de cómo toomodify el código para la nueva versión de hello, consulte documentación de Hola de Hola API específica.

