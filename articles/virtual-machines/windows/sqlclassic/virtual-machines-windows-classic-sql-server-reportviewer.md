---
title: aaaUse ReportViewer en un sitio Web | Documentos de Microsoft
description: "Este tema describe cómo toobuild un sitio Web de Microsoft Azure con control de ReportViewer de Visual Studio de Hola que muestra un informe almacenado en una máquina Virtual de Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Usar ReportViewer en un sitio web hospedado en Azure
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Puede crear un sitio Web de Microsoft Azure con hello control ReportViewer de Visual Studio que muestra un informe almacenado en una máquina Virtual de Microsoft Azure. Hola control ReportViewer está en una aplicación Web que se crea con hello plantilla aplicación Web ASP.NET.

> [!IMPORTANT]
> plantillas de aplicación Web ASP.NET MVC Hello no son compatibles con control de ReportViewer Hola.

tooincorporate ReportViewer en el sitio Web de Microsoft Azure, deberá hello toocomplete siguiente las tareas.

* **Agregar** toohello paquete de implementación de ensamblados
* **Configurar** autenticación y autorización
* **Publicar** Hola tooAzure de aplicación Web ASP.NET

## <a name="prerequisites"></a>Requisitos previos
Revise la sección "recomendaciones generales y prácticas recomendadas" de hello en [SQL Server Business Intelligence en máquinas virtuales Azure](../classic/ps-sql-bi.md).

> [!NOTE]
> Los controles ReportViewer se incluyen con Visual Studio, Standard Edition o superior. Si usas hello Web Developer Express Edition, debe instalar hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) características de tiempo de ejecución de ReportViewer toouse Hola.
> 
> No se admite el ReportViewer configurado en modo de procesamiento local en Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Agregar ensamblados toohello paquete de implementación
Si hospeda la aplicación ASP.NET en local, ensamblados de ReportViewer Hola normalmente se instala directamente en la caché de ensamblados global (GAC) de Hola Hola del servidor de IIS durante la instalación de Visual Studio y son accesibles directamente mediante la aplicación hello. Sin embargo, cuando se hospedan la aplicación ASP.NET en la nube de hello, Microsoft Azure no permite cualquier aplicación toobe instalada en Hola GAC, por lo que debe asegurarse de que los ensamblados de ReportViewer Hola están disponibles localmente para la aplicación. Puede hacerlo agregando toothem de referencias del proyecto y configurarlos toobe se copia localmente.

En el modo de procesamiento remoto, Hola control ReportViewer utiliza Hola siguientes ensamblados:

* **Microsoft.ReportViewer.WebForms.dll**: contiene código de ReportViewer hello, que necesita toouse ReportViewer en la página. Una referencia para este ensamblado se agrega tooyour proyecto cuando coloca un control ReportViewer en una página ASP.NET en el proyecto.
* **Microsoft.ReportViewer.Common.dll**: contiene las clases utilizadas por hello control ReportViewer en tiempo de ejecución. No se agrega automáticamente el proyecto de tooyour.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd un tooMicrosoft.ReportViewer.Common de referencia
* Haga clic en el proyecto **referencias** nodo y seleccione **Agregar referencia**, seleccione el ensamblado hello en la pestaña de .NET de Hola y haga clic en **Aceptar**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>ensamblados de hello toomake accesibles localmente por la aplicación ASP.NET
1. Hola **referencias** carpeta, haga clic en el ensamblado Microsoft.ReportViewer.Common de Hola para que sus propiedades aparecen en el panel de propiedades de Hola.
2. En el panel de propiedades de hello, establezca **Copy Local** tooTrue.
3. Repita los pasos 1 y 2 para Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget paquete de idioma de ReportViewer
1. Instale el correspondiente paquete redistribuible de Microsoft Report Viewer 2012 Runtime Hola de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Idioma de hello seleccione de la lista desplegable de Hola y página de Hola obtiene toohello redirigida correspondiente página del centro de descarga.
3. Haga clic en **descargar** descarga de hello toostart de ReportViewerLP.exe.
4. Después de descargar ReportViewerLP.exe, haga clic en **ejecutar** tooinstall inmediatamente, o haga clic en **guardar** toosave se tooyour equipo. Si hace clic en **guardar**, recordar Hola nombre de carpeta de Hola donde guardar archivo hello.
5. Busque la carpeta de Hola donde guardó el archivo hello. Haga clic con el botón secundario en ReportViewerLP.exe, haga clic en **Ejecutar como administrador**, y luego en **Sí**.
6. Después de ejecutar ReportViewerLP.exe, verá Hola c:\windows\assembly tiene archivos de recursos de hello **Microsoft.ReportViewer.Webforms.Resources** y **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure para el control de ReportViewer localizado
1. Descargue e instale el paquete redistribuible de Microsoft Report Viewer 2012 Runtime Hola por siguiente Hola anteriormente instrucciones especificadas.
2. Crear <language> asociados de carpeta Hola Hola de proyecto y copiar archivos de ensamblado de recursos. son Hello toobe de archivos de ensamblado de recursos copiado: **Microsoft.ReportViewer.Webforms.Resources.dll** y **Microsoft.ReportViewer.Common.Resources.dll**. Seleccione los archivos de ensamblado de recursos de Hola y en el panel de propiedades de hello, establezca **copiar tooOutput directorio** demasiado "**copiar siempre**".
3. Establecer Hola Culture y UICulture para proyecto de hello web. Para obtener más información sobre cómo tooset Hola referencia cultural y la referencia cultural de interfaz de usuario para una página Web ASP.NET, vea [Cómo: conjunto hello referencia cultural y la referencia cultural de interfaz de usuario para la globalización de páginas Web de ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Configuración de autenticación y autorización
Hola ReportViewer debe toouse las credenciales adecuadas tooauthenticate con el servidor de informes de Hola y credenciales Hola deben estar autorizadas por hello server tooaccess Hola de informes que desee. Para obtener información acerca de la autenticación, vea notas del producto hello [servidores de informes de máquina virtual en función de Microsoft Azure y control de Visor de informes de Reporting Services](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Publicar hello tooAzure de aplicación Web ASP.NET
Para obtener instrucciones sobre cómo publicar un tooAzure de aplicación Web de ASP.NET, vea [Cómo: migrar y publicar un tooAzure de aplicación Web de Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) y [empezar a trabajar con aplicaciones Web y ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Si Hola comando Agregar proyecto de implementación de Azure o agregar un proyecto de servicio de nube de Azure no aparece en el menú contextual de hello en el Explorador de soluciones, puede necesitar toochange de .NET framework de destino de Hola para hello proyecto too.NET Framework 4.
> 
> comandos de Hello dos proporcionan básicamente Hola la misma funcionalidad. Uno o hello otro comando aparecerán en el menú contextual de hello según la versión de Hola SDK de Microsoft Azure ha instalado.
> 
> 

## <a name="resources"></a>Recursos
[Informes de Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[Business Intelligence de SQL Server en Máquinas virtuales de Azure](../classic/ps-sql-bi.md)

[Usar PowerShell tooCreate un Azure VM con un modo de servidor de informes nativo](../classic/ps-sql-report.md)

