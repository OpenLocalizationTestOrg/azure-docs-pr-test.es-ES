---
title: "aaaCloud Cruiser y la integración de la API de facturación de Microsoft Azure | Documentos de Microsoft"
description: "Proporciona una perspectiva exclusiva del socio de facturación de Microsoft Azure Cloud Cruiser, en sus experiencias integrar hello las API de facturación de Azure en su producto.  Esto es especialmente útil para los clientes de Azure y de Cloud Cruiser que están interesados en usar o probar Cloud Cruiser para el paquete de Microsoft Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Integración de Cloud Cruiser y de las API de facturación de Microsoft Azure
Este artículo describe cómo información Hola recopilada de hello que API nueva de facturación de Microsoft Azure puede usarse en Cloud Cruiser para flujo de trabajo costo simulación y análisis.

## <a name="azure-ratecard-api"></a>API de RateCard de Azure
Hola API RateCard proporciona información de tasa de Azure. Tras la autenticación con las credenciales adecuadas de hello, puede consultar Hola API toocollect metadatos acerca de los servicios de hello disponibles en Azure, además de las tasas de hello asociadas con el identificador de oferta.

Hola siguiente es una respuesta de ejemplo a través de API de Hola que muestra los precios de Hola para hello A0 (Windows) instancia:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>TooAzure de interfaz de Cruiser API RateCard la nube
Cloud Cruiser puede aprovechar la información de la API RateCard de Hola de maneras diferentes. En este artículo, le mostraremos cómo puede resultarle toomake usado IaaS cargas de trabajo costo simulación y análisis.

toodemonstrate este caso de uso, imagine una carga de trabajo de varias instancias que se ejecutan en Microsoft Azure Pack (WAP). el objetivo de Hello es toosimulate esta misma carga de trabajo en Azure y calcular los costos de Hola de hacer este tipo de migración. En orden toocreate esta simulación, hay dos toobe tareas principales realizadas:

1. **Importación y proceso Hola servicio información recopilada de hello API RateCard.** Esta tarea también se realiza en los libros de hello, donde extraer Hola de hello API RateCard es tooa transformado y publicados nuevo plan de tarifas. Este nuevo plan de tarifas se usará en hello simulaciones tooestimate Hola precios de Azure.
2. **Normalización de servicios de WAP y servicios de Azure para IaaS** De forma predeterminada, los servicios de WAP se basan en recursos individuales (CPU, tamaño de memoria, tamaño de disco, etc.) mientras que los de Azure se basan en el tamaño de instancia (A0, A1, A2, etc.). Esta primera tarea pueden ser realizadas por el motor ETL de Cloud Cruiser, llama a los libros, donde estos recursos se pueden integrar en tamaños de instancias, servicios de la instancia de tooAzure análoga.

### <a name="import-data-from-hello-ratecard-api"></a>Importar datos de hello API RateCard
Cloud Cruiser libros proporcionan una forma automatizada toocollect y proceso de la información de hello API RateCard.  Los libros ETL (extracción, transformación y carga) le permiten colección de hello tooconfigure, transformación y publicación de datos en base de datos de nube Cruiser Hola.

Cada libro puede tener una o varias colecciones, permitiéndole toocorrelate información de orígenes diferentes toocomplement o aumentar los datos de uso de Hola. Hola siguiendo dos pantallas muestran cómo toocreate un nuevo *colección* en un libro existente e importar información en hello *colección* de hello API RateCard:

![Ilustración 1 - Creación de una nueva colección][1]

![Figura 2: importar datos desde la nueva colección de Hola][2]

Después de importar datos de hello en libro hello, es posible toocreate varios pasos y procesos de transformación, toomodify y modelo Hola datos. En este ejemplo, puesto que sólo estamos interesados en infraestructura como-servicio (IaaS), podemos usar Hola transformación pasos tooremove las filas innecesarias o registros, relacionados con tooservices distinto de IaaS.

Hello captura de pantalla siguiente muestra los pasos de transformación de hello usan datos de hello tooprocess recopilados a través de API RateCard:

![Figura 3 - transformación pasos tooprocess recopilan datos a través de API RateCard][3]

### <a name="defining-new-services-and-rate-plans"></a>Definición de nuevos servicios y planes de tarifas
Hay servicios de toodefine de distintas maneras en Cruiser en la nube. Una de las opciones de hello es tooimport servicios de Hola Hola de datos de uso. Este método se utiliza normalmente cuando se trabaja con nubes públicas, donde servicios Hola ya están definidos por el proveedor de Hola.

Un Plan de tarifas es un conjunto de tipos de cambio o los precios que pueden ser servicios toodifferent aplicado, en función de las fechas de vigencia o grupo de clientes, entre otras opciones. Planes de velocidad también pueden utilizarse en escenarios de "What-if", toounderstand o simulación de toocreate Cruiser de nube cómo los cambios en los servicios pueden afectar al costo total de Hola de una carga de trabajo.

En este ejemplo, se usará información de servicio de Hola de nuevos servicios de hello API RateCard toodefine en Cruiser en la nube. Hola igual manera, podemos usar tarifas Hola asociadas toohello services toocreate un nuevo Plan de tarifas en Cruiser en la nube.

Al final de Hola de proceso de transformación de hello, es posible toocreate un nuevo paso y publicar datos de Hola de hello API RateCard como las tasas y nuevos servicios.

![Figura 4: publicar datos de Hola de hello API RateCard como nuevos servicios y las tasas][4]

### <a name="verify-azure-services-and-rates"></a>Comprobación de servicios y tarifas de Azure
Después de publicar servicios de Hola y tasas, puede comprobar lista de Hola de importados servicios de nube Cruiser *servicios* ficha:

![Figura 5 - comprobar Hola nuevos servicios][5]

En hello *velocidad planes* ficha, puede comprobar el nuevo plan de tarifas Hola denominado "AzureSimulation" con las tasas de hello importado de hello API RateCard.

![Figura 6 - comprobar Hola nuevo Plan de tarifas y tasas de asociados][6]

### <a name="normalize-wap-and-azure-services"></a>Normalización de servicios de WAP y de Azure
De forma predeterminada, WAP proporciona información de uso según el uso de Hola de proceso, memoria y recursos de red. En Cruiser en la nube, puede definir la asignación de hello directamente en los servicios en función o medido uso de estos recursos. Por ejemplo, puede establecer una velocidad básica para cada hora de uso de CPU o cargo Hola GB de memoria asignada tooan instancia.

En este ejemplo, en los costos de toocompare de orden entre WAP y Azure, necesitamos tooaggregate Hola el uso de recursos WAP en paquetes, que, a continuación, puede ser servicios tooAzure asignada. Esta transformación se puede implementar fácilmente en los libros de hello:

![Figura 7: transformar toonormalize servicios de datos de WAP][7]

Hola último paso en el libro de hello es datos de hello toopublish en base de datos de nube Cruiser Hola. Durante este paso, los datos de uso de hello ahora está integrados en los servicios (que se asignan toohello servicios de Azure) y ligada cargos de toodefault tasas toocreate Hola.

Después de libro Hola acabado, puede automatizar el procesamiento de Hola de datos de hello, agregando una tarea en el programador de Hola y especificando Hola frecuencia y la hora de hello libro toorun.

![Ilustración 8 - Programación de libros][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Creación de informes para análisis de simulación de costos de cargas de trabajo
Después de que se recopila el uso de Hola y cargos se cargan en la base de datos de nube Cruiser Hola, podemos aprovechar Hola visión de Cloud Cruiser módulo toocreate Hola cargas de trabajo costo simulación que se desee.

En orden toodemonstrate este escenario, hemos creado Hola después de informe:

![Comparación de costos][9]

gráfico de Hello superior muestra una comparación de costo por servicios, comparar los precios de Hola de ejecución carga de trabajo de Hola para cada servicio específico de WAP (azul oscuro) y Azure (azul claro).

gráfico de la parte inferior de Hello muestra hello datos mismo pero desglosado por departamento. Esto muestra los costes de Hola para cada departamento toorun sus cargas de trabajo en WAP y Azure, junto con la diferencia de hello entre ellas en la barra de ahorro de hello (verde).

## <a name="azure-usage-api"></a>API de uso de Azure
### <a name="introduction"></a>Introducción
Microsoft presentó recientemente Hola API de uso de Azure, permitir a los suscriptores tooprogrammatically extracción de información de toogain de datos de uso en su consumo. Esto es muy bien para los clientes de Cruiser en la nube que puede aprovechar las ventajas de hello más rico conjunto de datos disponible a través de esta API.

Cloud Cruiser puede Aproveche la integración de hello con hello API de uso de varias maneras. Hola granularidad (información de uso por hora) y la información de metadatos de recursos disponible a través de hello que proporciona API Hola conjunto de datos es necesario toosupport flexible gastos o anulación modelos. 

En este tutorial, presentamos un ejemplo de cómo Cloud Cruiser pueden beneficiarse de hello información sobre las API de uso. Más concretamente, se crea un grupo de recursos en Azure, asociar etiquetas de estructura de la cuenta de hello y describen Hola proceso de extracción y procese la información de etiqueta de hello en Cloud Cruiser.

objetivo final de Hello es toobe toocreate capaz de informes como Hola sigue uno y ser capaz de tooanalyze coste y consumo basado en la estructura de cuenta de hello rellenado por etiquetas de Hola.

![Ilustración 10 - Informe con desgloses usando etiquetas][10]

### <a name="microsoft-azure-tags"></a>Etiquetas de Microsoft Azure
datos de Hello disponibles a través de hello API de uso de Azure incluyen no solo la información sobre el consumo, sino también los metadatos de recursos, incluidas las etiquetas asociadas con él. Etiquetas proporcionan una manera sencilla de tooorganize los recursos, pero en orden toobe eficaz, debe tooensure que:

* Las etiquetas son recursos de toohello aplicado correctamente en tiempo de aprovisionamiento
* Las etiquetas se usan correctamente en hello gastos/contracargo proceso tootie Hola uso toohello estructura de la organización cuenta.

Estos requisitos pueden ser desafiantes, especialmente cuando hay un proceso manual de aprovisionamiento de Hola o cargando lado. Al introducir incorrectamente, incorrectas o incluso faltan etiquetas son quejas más habituales de los clientes cuando con etiquetas y estos errores, puede tomar vida en hello está cargando lado muy difícil.

Con hello nueva API de uso de Azure, Cloud Cruiser puede extraer información de etiquetado de recursos y a través de una sofisticada herramienta ETL denominada libros, corregir estos errores de etiquetado comunes. Mediante la transformación mediante expresiones regulares y correlación de datos, Cruiser de nube puede identificar recursos etiquetados incorrectamente y aplicar etiquetas correctas de hello, asegurándose de asociación correcta Hola de recursos de hello con consumidor Hola.

En Hola está cargando lado Cloud Cruiser automatiza Hola gastos/contracargo proceso y pueden aprovechar Hola etiqueta información tootie Hola uso toohello consumidor adecuado (departamento, división, proyecto, etcetera). Esta automatización proporciona una enorme mejora y puede garantizar un proceso de cobro coherente y auditable.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Creación de un grupo de recursos con etiquetas en Microsoft Azure
Hello primer paso en este tutorial es toocreate un grupo de recursos en hello portal de Azure, a continuación, crear nuevas etiquetas tooassociate toohello recursos. En este ejemplo, se crearán Hola siguientes etiquetas: departamento, entorno, propietario, proyecto.

Hola de captura de pantalla siguiente muestra un ejemplo de que etiquetas de grupo de recursos con hello asociados.

![Ilustración 11 - Grupo de recursos con etiquetas asociadas en Azure Portal][11]

Hola siguiente paso es información de Hola de toopull de hello API de uso en Cruiser en la nube. Hola API de uso actualmente proporciona respuestas en formato JSON. Este es un ejemplo de Hola los datos recuperados:

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Importar datos de API de uso de hello en Cloud Cruiser
Cloud Cruiser libros proporcionan una forma automatizada toocollect y proceso de la información de hello API de uso. Un libro ETL (extracción, transformación y carga) le permite tooconfigure colección de hello, transformación y publicación de datos en base de datos de nube Cruiser Hola.

Cada libro puede tener una o varias colecciones. Esto le permite toocorrelate información de datos de uso de saludo de toocomplement o ampliar orígenes diferentes. En este ejemplo, crearemos una nueva hoja en el libro de la plantilla de Azure de hello (*UsageAPI)* y establecer una nueva *colección* tooimport información de hello API de uso.

![Figura 3: datos de uso de la API importados en la hoja de hello UsageAPI][12]

Observe que este libro ya tiene otro hojas tooimport servicios de Azure (*ImportServices*) y procesar la información de consumo de Hola de hello Billing API (*PublishData*).

A continuación utilizaremos Hola Hola de toopopulate de API de uso *UsageAPI* hoja e información de hello poner en correlación con los datos de consumo de Hola de hello Billing API sobre hello *PublishData* hoja.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Procesar la información de etiqueta Hola de hello API de uso
Después de importar datos de hello en libro hello, crearemos los pasos de transformación en hello *UsageAPI* hoja de información del pedido tooprocess Hola de hello API. Primer paso es toouse un Hola de tooextract de procesador "División de JSON" etiquetas de un solo campo, a continuación, crear campos para cada uno de ellos (departamento, proyecto, propietario y entorno).

![Figura 4: crear nuevos campos para obtener información de etiqueta de Hola][13]

Hola aviso "Redes" servicio falta información de etiqueta de hello (cuadro amarillo), pero que podamos comprobar que es parte del programa Hola mismo grupo de recursos examinando hello *ResourceGroupName* campo. Puesto que tenemos las etiquetas de Hola para hello otros recursos de este grupo de recursos, podemos usar esta Hola de tooapply de información que falta el recurso de etiquetas toothis más adelante en el proceso de Hola.

siguiente paso Hello es toocreate una información de hello asociar la tabla búsqueda de hello etiquetas toohello *ResourceGroupName*. Esta tabla de búsqueda se usará en hello siguiente paso tooenrich Hola consumo de datos con información de etiqueta.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Agregar datos de consumo de hello etiqueta información toohello
Ahora podemos pasamos toohello *PublishData* hoja, qué procesos Hola información sobre el consumo de hello Billing API y agregar campos de hello extraídos de etiquetas de Hola. Este proceso se realiza examinando la tabla de búsqueda de hello creada en el paso anterior de hello, con hello *ResourceGroupName* como clave de Hola para búsquedas de Hola.

![Figura 5 - rellenar la estructura de la cuenta de hello con información de Hola de búsquedas de Hola][14]

Tenga en cuenta que se aplicaron los campos de estructura de hello cuenta adecuada para el servicio de "Red" Hola, corregir el problema de hello con hello faltan etiquetas. Se rellenan también campos de estructura de la cuenta de hello para los recursos que no sea el grupo de recursos de destino "Sí", en orden toodifferentiate informa de ellos en Hola.

Ahora tenemos tooadd un paso toopublish Hola uso de datos. Durante este paso, los tipos adecuados para cada servicio definido en el Plan de tarifas Hola será la información de uso de toohello aplicado, con cargo resultante Hola cargado en la base de datos de Hola.

Hola mejor parte es que solo tiene una vez toogo a través de este proceso. Cuando se completa el libro de hello, basta con tooadd se toohello programador y se ejecutan cada hora o diariamente en hello hora programada. A continuación, es simplemente cuestión de crear nuevos informes o personalizar las existentes, en orden tooanalyze hello tooget significativo información sobre los datos de su uso en la nube.

### <a name="next-steps"></a>Pasos siguientes
* Para obtener instrucciones detalladas sobre la creación de Cloud Cruiser libros e informes, consulte la en línea tooCloud Cruiser [documentación](http://docs.cloudcruiser.com/) (inicio de sesión válido necesario).  Para obtener más información acerca de Cloud Cruiser, póngase en contacto con [info@cloudcruiser.com](mailto:info@cloudcruiser.com).
* Vea [obtener información sobre el consumo de recursos de Microsoft Azure](billing-usage-rate-card-overview.md) para obtener información general de uso de recursos de Azure de Hola y RateCard APIs.
* Extraer del repositorio hello [referencia de API de REST de facturación de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) para obtener más información sobre las API, que forman parte del conjunto de Hola de las API proporcionadas por hello Azure Resource Manager.
* Si desea que toodive directamente en el código de ejemplo de Hola, visite nuestros ejemplos código de API de facturación de Azure de Microsoft en [ejemplos de código de Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Más información
* Vea hello [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) artículo toolearn más información acerca de hello Azure Resource Manager.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Ilustración 1 - Creación de una nueva colección"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figura 2: importar datos desde la nueva colección de Hola"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figura 3 - transformación pasos tooprocess recopilan datos a través de API RateCard"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figura 4: publicar datos de Hola de hello API RateCard como nuevos servicios y las tasas"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figura 5 - comprobar Hola nuevos servicios"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figura 6 - comprobar Hola nuevo Plan de tarifas y tasas de asociados"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figura 7: transformar toonormalize servicios de datos de WAP"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Ilustración 8 - Programación de libros"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figura 9 - informe de ejemplo para el escenario de comparación de costo de carga de trabajo de Hola"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Ilustración 10 - Informe con desgloses usando etiquetas"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Ilustración 11 - Grupo de recursos con etiquetas asociadas en Azure Portal"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figura 12 - los datos de uso de la API importados en hoja de hello UsageAPI"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figura 13 - crear nuevos campos para obtener información de etiqueta de Hola"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Figura 14 - rellenar la estructura de la cuenta de hello con información de Hola de búsquedas de Hola"
