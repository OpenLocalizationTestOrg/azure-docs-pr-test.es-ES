---
title: soluciones de aaaUse API de lote de Azure y herramientas toodevelop a gran escala procesamiento en paralelo | Documentos de Microsoft
description: "Obtenga información acerca de hello las API y las herramientas disponibles para desarrollar soluciones con el servicio de Azure Batch Hola."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Información general sobre las API y herramientas de Batch

Procesamiento paralelo cargas de trabajo con Azure Batch suele realizarla mediante programación utilizando uno de hello [API de lote](#batch-development-apis). La aplicación de cliente o servicio puede usar hello las API de lote toocommunicate con hello servicio por lotes. Con hello las API de lote, puede crear y administrar grupos de nodos de ejecución, máquinas virtuales o servicios en la nube. A continuación, puede programar toorun trabajos y tareas en esos nodos. 

Eficazmente puede procesar las cargas de trabajo a gran escala para su organización, o proporcionar un front-end de servicio a los clientes de tooyour para que se pueden ejecutar trabajos y tareas--a petición o según una programación--en uno, cientos o incluso miles de nodos. Azure Batch también se puede usar como parte de un flujo de trabajo mayor, administrado mediante herramientas como [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Cuando esté listo toodig en toohello API de lote para una descripción más detallada de hello presenta lo proporciona, desproteger hello [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Cuentas de Azure para desarrollo con Batch
Cuando se desarrollan soluciones de lote, deberá usar Hola siguiendo las cuentas de Microsoft Azure.

* **Cuenta de Azure y suscripción**: si aún no tiene ninguna suscripción a Azure, puede activar su [ventaja como suscriptor de MSDN][msdn_benefits] o bien registrarse para obtener una [cuenta gratuita de Azure][free_account]. Al crear una cuenta, se crea automáticamente una suscripción predeterminada.
* **Cuenta de Batch**: los recursos de Azure Batch, entre los que se incluyen grupos, nodos de proceso, trabajos y tareas, están asociados a una cuenta de Azure Batch. Cuando la aplicación realiza una solicitud contra Hola servicio por lotes, autentica solicitud hello mediante nombre de cuenta de Azure Batch hello, dirección URL de Hola de cuenta de hello y una clave de acceso. También puede [crear cuenta de lote](batch-account-create-portal.md) Hola portal de Azure.
* **Cuenta de Storage**: Batch incluye compatibilidad integrada para trabajar con archivos en [Azure Storage][azure_storage]. Casi cada escenario de lote utiliza almacenamiento de blobs de Azure para programas de Hola que se ejecutan las tareas y los datos de Hola que procesan de almacenamiento provisional y para el almacenamiento de Hola de datos de salida que generan. toocreate una cuenta de almacenamiento, consulte [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>API del servicio Batch

Las aplicaciones y servicios pueden emitir llamadas directas de API de REST o usar uno o varios de hello después toorun de bibliotecas de cliente y administrar las cargas de trabajo de lote de Azure.

| API | Referencia de API | Descargar | Tutorial | Ejemplos de código | Más información |
| --- | --- | --- | --- | --- | --- |
| **REST de Lote** |[MSDN][batch_rest] |N/D |- |- | [Versiones compatibles](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **.NET de Lote** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Tutorial](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Notas de la versión](http://aka.ms/batch-net-dataplane-changelog) |
| **Batch Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Tutorial](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Léame](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Léame](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[Léame][api_sample_java] | [Léame](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>API de administración de Batch

Hola API del Administrador de recursos de Azure para lote proporcionan acceso mediante programación tooBatch cuentas. Con estas API, se pueden administrar mediante programación cuentas, cuotas y paquetes de aplicaciones de Batch.  

| API | Referencia de API | Descargar | Tutorial | Ejemplos de código |
| --- | --- | --- | --- | --- |
| **REST de Resource Manager de Batch** |[docs.microsoft.com][api_rest_mgmt] |N/D |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **.NET de Resource Manager de Batch** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Tutorial](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Herramientas de línea de comandos de Batch

Estas herramientas de línea de comandos proporcionan Hola la misma funcionalidad como Hola servicio por lotes y las API de administración de proceso por lotes: 

* [Cmdlets de PowerShell de lote][batch_ps]: Hola cmdlets de Azure Batch en hello [Azure PowerShell](/powershell/azure/overview) módulo habilitar recursos de proceso por lotes toomanage con PowerShell.
* [CLI de Azure](/cli/azure/overview): hello Azure interfaz de línea de comandos (CLI de Azure) es un conjunto de herramientas multiplataforma que proporciona los comandos de shell para interactuar con muchos de los servicios de Azure, incluido el servicio de lote de Hola y el servicio de administración de lotes. Vea [recursos administrar lote con Azure CLI](batch-cli-get-started.md) para obtener más información acerca del uso de hello CLI de Azure con el lote.

## <a name="other-tools-for-application-development"></a>Otras herramientas de desarrollo de aplicaciones

Estas son algunas herramientas adicionales que pueden ser útiles para crear y depurar los servicios y aplicaciones de Batch:

* [Portal de Azure][portal]: puede crear, supervisar y eliminar grupos por lotes, los trabajos y tareas en hello Azure hojas de lote del portal. Puede ver información de estado de Hola para estos y otros recursos mientras ejecuta los trabajos e incluso descargar archivos desde los nodos de proceso de hello en los grupos. Por ejemplo, puede descargar el archivo `stderr.txt` de una tarea con errores mientras soluciona problemas. También puede descargar los archivos de escritorio remoto (RDP) que puede usar toolog en nodos de toocompute.
* [El Explorador de lote Azure][batch_explorer]: lote explorador proporciona funcionalidad de administración de recursos de proceso por lotes similar como Hola portal de Azure, pero en una aplicación de cliente de Windows Presentation Foundation (WPF) independiente. Una de las aplicaciones de ejemplo de Hola .NET de lote disponible en [GitHub][github_samples], genérelo con Visual Studio 2015 o versiones más recientes y usar toobrowse y administrar recursos de hello en su cuenta de lote mientras desarrolla y depurar las soluciones de lote. Ver trabajo, grupo y detalles de la tarea, descargar archivos de nodos de proceso y conectan toonodes de forma remota mediante el uso de archivos de escritorio remoto (RDP) que puede descargar con el Explorador de lote.
* [Microsoft Azure Storage Explorer][storage_explorer]: mientras no es estrictamente una herramienta de Azure Batch, Hola Explorador de almacenamiento es la toohave de otra herramienta útil mientras desarrolla y depurar las soluciones de lote.

## <a name="additional-resources"></a>Recursos adicionales

- toolearn acerca de los eventos de registro de la aplicación por lotes, vea [registrar eventos de evaluación de diagnóstico y supervisión de soluciones de lote](batch-diagnostics.md). Para ver una referencia de eventos generados por hello servicio por lotes, vea [análisis por lotes](batch-analytics.md).
- Para más información acerca de las variables de entorno para nodos de proceso, consulte [Variables de entorno de nodos de proceso de Azure Batch](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Pasos siguientes

* Hola de lectura [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md), información esencial para todo aquel que preparar toouse por lotes. artículo de Hello contiene información más detallada sobre los recursos del servicio por lotes como hello, nodos, trabajos y las tareas y grupos de muchas características de la API que puede usar al compilar la aplicación de lote.
* [Empezar a trabajar con la biblioteca de hello Azure Batch para .NET](batch-dotnet-get-started.md) toolearn cómo toouse C# y Hola tooexecute de biblioteca .NET de lotes en una carga de trabajo simple con un flujo de trabajo comunes de lote. En este artículo debe ser uno de su primera detiene mientras aprende cómo toouse Hola servicio por lotes. También hay un [versión de Python](batch-python-tutorial.md) de tutorial Hola.
* Descargar hello [ejemplos en GitHub de código] [ github_samples] toosee cómo C# y Python puedan interactuar con las cargas de trabajo de ejemplo de tooschedule y proceso de lote.
* Extraer del repositorio hello [ruta de acceso de aprendizaje por lotes] [ learning_path] tooget una idea de hello recursos disponibles tooyou que obtenga información acerca de toowork con el lote.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
