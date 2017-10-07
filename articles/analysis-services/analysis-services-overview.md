---
title: aaaWhat es Azure Analysis Services | Documentos de Microsoft
description: Obtener panorama general de Hola de Analysis Services en Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>¿Qué es Azure Analysis Services?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services proporciona en la nube de Hola de modelado de datos de nivel empresarial. Es una plataforma totalmente administrada como servicio (PaaS), que se integra con los servicios de la plataforma de datos de Azure. 

Con Analysis Services, puede combinar datos de diversos orígenes, definir métricas y proteger los datos en un modelo de datos semántico único y de confianza. modelo de datos de Hello proporciona una manera más fácil y rápida para su toobrowse usuarios grandes cantidades de datos con las aplicaciones cliente como Power BI, Excel, Reporting Services, aplicaciones de terceros y personalizadas.

![Orígenes de datos](./media/analysis-services-overview/aas-overview-data-sources.png)

Extraer del repositorio [este vídeo](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) global de toolearn cómo se ajusta Azure Analysis Services con Microsoft capacidades de BI y cómo puede beneficiarse de obtención de los modelos de datos en la nube de Hola.

## <a name="built-on-sql-server-analysis-services"></a>Basado en SQL Server Analysis Services
Azure Analysis Services es compatible con muchas de las estupendas características que ya se encuentran en SQL Server Analysis Services Enterprise Edition. Azure Analysis Services es compatible con los modelos tabulares en hello 1200 y 1400 [niveles de compatibilidad](analysis-services-compat-level.md). Se admiten todas las traducciones, particiones, seguridad de nivel de fila y relaciones bidireccionales. Los modos In-memory y DirectQuery permiten consultas increíblemente rápidas en conjuntos de datos enormes y complejos.

Los modelos tabulares ofrecen un desarrollo rápido y son altamente personalizables. Para los desarrolladores, los modelos tabulares incluyen objetos de modelo de toodescribe de modelo de objeto Tabular (TOM) Hola. TOM se expone en JSON a través de hello [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) hello lenguaje de definición de datos AMO a través de Hola y [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) espacio de nombres.

## <a name="better-with-azure"></a>Mejor con Azure
Azure Analysis Services se integra con muchos servicios de Azure, permitiéndole toobuild sofisticadas soluciones de análisis. Integración con [Azure Active Directory](../active-directory/active-directory-whatis.md) proporciona acceso seguro basado en roles tooyour los datos críticos. Integrar con [Data Factory de Azure](../data-factory/data-factory-introduction.md) canalizaciones mediante la inclusión de una actividad que carga datos en el modelo de Hola. [Azure Automation](../automation/automation-intro.md) y [Azure Functions](../azure-functions/functions-overview.md) se pueden usar para realizar una orquestación ligera de modelos mediante código personalizado.

## <a name="get-up-and-running-quickly"></a>Póngase rápidamente a pleno funcionamiento
Con Azure Portal, puede [crear un servidor](analysis-services-create-server.md) en minutos. Además, con las [plantillas](../azure-resource-manager/resource-manager-create-first-template.md) de Azure Resource Manager y PowerShell, puede aprovisionar servidores mediante una plantilla declarativa. Con una única plantilla, puede implementar varios servicios junto con otros componentes de Azure como las cuentas de almacenamiento y Azure Functions. 

Una vez que haya creado un servidor, puede crear un modelo tabular directamente en Azure Portal. Con hello nueva (versión preliminar) [las características del Diseñador Web](analysis-services-create-model-portal.md), puede conectarse tooan base de datos de SQL de Azure, origen de datos de almacenamiento de datos de SQL Azure, o importar un archivo .pbix de Power BI Desktop. Las relaciones entre tablas se crean automáticamente, y puede crear medidas o editar el archivo model.bim de hello en formato json derecha desde el explorador.

## <a name="scale-tooyour-needs"></a>Escala tooyour necesidades
Azure Analysis Services está disponible en los niveles Desarrollador, Básico y Estándar. Dentro de cada nivel, los costos de plan varían en tamaño de alimentación, QPUs y memoria de tooprocessing correspondiente. Cuando cree un servidor, seleccione un plan dentro de un nivel. Puede cambiar los planes de o hacia abajo en hello mismo nivel o tooa actualización de nivel superior, pero no se puede cambiar de un nivel inferior de tooa de nivel superior.

Escale o reduzca verticalmente, o pause el servidor. Utilice Hola portal de Azure o tienen control total sobre la marcha mediante PowerShell. Pague solo por lo que usa. toolearn más información acerca de los distintos planes de Hola y niveles y use Hola precios calculadora toodetermine Hola plan adecuado para usted, consulte [precios de Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Mantener los datos a mano
Se pueden crear servidores de Analysis Services Azure siguiente hello [regiones de Azure](https://azure.microsoft.com/regions/):

| América | Europa | Asia Pacífico |
|----------|--------|--------------|
|  Sur de Brasil<br> Centro de Canadá<br> Este de EE. UU. 2<br> Centro-Norte de EE. UU<br> Centro-Sur de EE. UU<br> Centro occidental de EE.UU.<br> Oeste de EE. UU. | Europa del Norte<br> Sur del Reino Unido<br> Europa occidental |   Sudeste de Australia<br> Este de Japón<br> Sudeste asiático<br> Oeste de la India  |

Nuevas regiones añadidas todo el tiempo de hello, por lo que esta lista puede estar incompleta. Elija una ubicación cuando cree el servidor en Azure Portal o mediante las plantillas de Azure Resource Manager. Hola tooget el mejor rendimiento, elija una ubicación más cercana a su base de usuarios más grande. Garantice una [alta disponibilidad](analysis-services-bcdr.md) mediante la implementación de los modelos en servidores redundantes de varias regiones.

## <a name="migrate-your-existing-tabular-models"></a>Migración de los modelos tabulares existentes
Si ya tiene soluciones de modelos de Analysis Services de SQL Server local existentes, puede migrar tooAzure Analysis Services sin cambios significativos. toomigrate, puede usar SSDT toodeploy el servidor de tooyour de modelo. O bien, en SSMS, puede usar un proceso de copia de seguridad y restauración o TMSL.

Si tiene orígenes de datos locales, necesita tooinstall y configurar un [puerta de enlace de datos local](analysis-services-gateway.md). Si tiene roles y los miembros del rol ya configurados, migración sus roles, pero tiene los miembros del rol tooreadd con SSMS o PowerShell.

## <a name="connect-toopopular-data-sources"></a>Conectarse a orígenes de datos de toopopular
Azure Analysis Services admite [conectar orígenes toodata](analysis-services-datasource.md) local de su organización y en la nube de Hola. Combine datos de orígenes de datos tanto locales como en la nube para crear una solución híbrida. 

Nuevos modelos tabulares de 1400 usar característica de obtener datos moderna de hello en SSDT, basado en el lenguaje de fórmulas de consulta de hello M. Con obtener datos, tienen más de transformación de datos y características de mashup y toocreate de capacidad de Hola y editar sus propias consultas de lenguaje de fórmulas de M avanzadas. Por ejemplo, con los modelos tabulares 1400, puede modelar en archivos de datos de Azure Blob Storage.

## <a name="use-hello-tools-you-already-know"></a>Usar herramientas de Hola que ya conoce

![Herramientas para desarrolladores de BI](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) para Visual Studio
Desarrollar e implementar modelos con hello libre [SQL Server Data Tools (SSDT) para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). SSDT incluye plantillas de proyecto de Analysis Services que le permiten ponerse rápidamente a pleno funcionamiento. SSDT incluye ahora Hola moderna obtener datos origen de datos de consultas y mashup funcionalidad para los modelos tabulares 1400. Si está familiarizado con obtener datos en Power BI Desktop y Excel 2016, ya sabe lo fácil que es toocreate altamente personalizadas consultas de origen de datos.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
Administrar los servidores y las bases de datos modelo mediante el uso de [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Conectar servidores tooyour en la nube de Hola. Ejecutar scripts TMSL derecha de la ventana de consulta XMLA de Hola y automatizar tareas mediante los scripts de TMSL. Surgen nuevas características y funcionalidades con gran rapidez: SSMS se actualiza mensualmente.

#### <a name="powershell"></a>PowerShell
Tareas de administración de recursos de servidor como la creación de servidores, suspender o reanudar las operaciones del servidor o cambiar el nivel de servicio de hello (nivel) usan cmdlets de Azure Resource Manager (AzureRM). Otras tareas para administrar las bases de datos como agregar o quitar miembros del rol, procesar o ejecutar scripts TMSL usar cmdlets de módulo de SqlServer Hola. Módulos AzureRM y SQL Server están disponibles en hello [Galería de PowerShell](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Los datos están seguros
![Visualizaciones de datos](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Autenticación
La autenticación de usuarios para Azure Analysis Services se realiza mediante [Azure Active Directory (AD)](../active-directory/active-directory-whatis.md). Cuando se intente toolog en base de datos de tooan Azure Analysis Services, el uso de los usuarios una identidad de cuenta de organización con la base de datos de access toohello está tratando de tooaccess. Estas identidades de usuario deben ser miembros del predeterminado de hello Azure Active Directory para la suscripción de Hola donde reside el servidor de Analysis Services de Azure de Hola. más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).

#### <a name="data-security"></a>Seguridad de los datos
Azure Analysis Services utiliza el almacenamiento de toopersist de almacenamiento de blobs de Azure y los metadatos de las bases de datos de Analysis Services. Los archivos de datos en Blob se cifran mediante cifrado de lado servidor (SSE) de Azure Blob. Cuando se usa el modo de consulta directa, se almacenan solo metadatos. se tiene acceso a los datos reales de Hola Hola origen de datos en tiempo de consulta.

#### <a name="on-premises-data-sources"></a>Orígenes de datos locales
Acceso seguro toodata que residen localmente en su organización se consigue instalando y configurando un [puerta de enlace de datos local](analysis-services-gateway.md). Las puertas de enlace proporcionan acceso toodata para consulta directa y modos de en memoria. Cuando un modelo Azure Analysis Services conecta a origen de datos de tooan local, se crea una consulta junto con las credenciales de hello cifrada para el origen de datos de hello local. servicio de nube de puerta de enlace de Hello analiza la consulta de Hola e inserta Hola solicitud tooan Service Bus de Azure. puerta de enlace de Hello local sondea hello Azure Service Bus para las solicitudes pendientes. puerta de enlace de Hello obtiene Hola consulta, descifra las credenciales de Hola y conecta el origen de datos de toohello para su ejecución. Hola resultados son, a continuación, envía desde el origen de datos de hello, realizar copias de puerta de enlace de toohello y, a continuación, en los servicios de análisis de Azure toohello base de datos.

Los servicios de análisis de Azure se rige por hello [condiciones de Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) hello y [declaración de privacidad de Microsoft Online Services](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn más información acerca de la seguridad de Azure, vea hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Compatible con las herramientas de cliente más recientes de Hola
![Visualizaciones de datos](./media/analysis-services-overview/aas-overview-clients.png)

Las modernas herramientas de exploración y visualización de datos como Power BI, Excel y otras herramientas de terceros, proporcionan a los usuarios una información interactiva, enriquecida visualmente, sobre los datos del modelo.

Los clientes usan MSOLAP, AMO o ADOMD [bibliotecas de cliente](analysis-services-data-providers.md) servidores de servicios de tooconnect tooAnalysis. Las aplicaciones cliente de Microsoft, como Power BI Desktop y Excel, instalan las tres bibliotecas de cliente. Pero tenga en cuenta, según la versión de Hola o la frecuencia de las actualizaciones, las bibliotecas de cliente no pueden ser versiones más recientes de hello requeridas por los servicios de análisis de Azure. Hello mismo aplica toocustom aplicaciones u otras interfaces, como AsCmd, TOM, ADOMD.NET. Normalmente, estas aplicaciones necesitan instalar manualmente las bibliotecas de hello como parte de un paquete.


## <a name="get-help"></a>Obtener ayuda

#### <a name="documentation"></a>Documentación
Azure Analysis Services es toomanage y tooset simple seguridad. Puede encontrar toda la información del Hola necesita toocreate y administrar los servicios del servidor. Al crear un servidor de tooyour de toodeploy de modelo de datos, ha mucho Hola igual como para crear un modelo de datos se implementa tooan local servidor. Hay una amplia biblioteca de artículos sobre conceptos, procedimientos, tutoriales y referencia en [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services).

#### <a name="videos"></a>Vídeos
Consulte algunos vídeos útiles en [Azure Analysis Services en Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services).

#### <a name="blogs"></a>Blogs
Las cosas cambian rápidamente. Siempre puede obtener información más reciente de hello en hello [blog del equipo de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/) y [blog de Azure](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Comunidad
Analysis Services cuenta con una dinámica comunidad de usuarios. Unir conversación hello en [foro de Azure Analysis Services](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Comentarios
¿Tiene sugerencias o solicitudes de características? Estar seguro tooleave sus comentarios en [Azure Analysis Services comentarios](https://aka.ms/azureanalysisservicesfeedback).

¿Tiene sugerencias acerca de la documentación de hello? Puede agregar comentarios con Livefyre en parte inferior de Hola de cada artículo.

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe más acerca de los servicios de análisis de Azure, es hora de tooget iniciado. Obtenga información acerca de cómo demasiado[crear un servidor](analysis-services-create-server.md) en Azure. Cuando el servidor está listo, paso a través de hello [tutorial de Adventure Works](tutorials/aas-adventure-works-tutorial.md) toolearn cómo toocreate un modelo tabular totalmente funcional e implementarlo tooyour server.
