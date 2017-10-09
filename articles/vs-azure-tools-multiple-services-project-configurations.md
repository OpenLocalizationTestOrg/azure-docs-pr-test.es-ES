---
title: aaaConfiguring su proyecto de Azure mediante varias configuraciones del servicio | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure un Azure cloud proyecto de servicio cambiando los archivos de hello ServiceDefinition.csdef y ServiceConfiguration.cscfg."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Configuración de su proyecto Azure mediante varias configuraciones de servicio
Un proyecto de servicio en la nube de Azure incluye dos archivos de configuración: ServiceDefinition.csdef y ServiceConfiguration.cscfg. Estos archivos están empaquetados con la aplicación de servicio de nube de Azure e implementan tooAzure.

* Hola **ServiceDefinition.csdef** archivo contiene los metadatos de hello requerido por hello entorno de Azure para los requisitos de saludo de la aplicación de servicio de nube, incluidos los roles que contiene. Este archivo también contiene los valores de configuración que se aplican tooall instancias. Estos valores de configuración se pueden leer en tiempo de ejecución mediante Hola API de tiempo de ejecución de hospedaje de servicios de Azure. Este archivo no se puede actualizar mientras el servicio se ejecuta en Azure.
* Hola **ServiceConfiguration.cscfg** archivo establece valores para los valores de configuración de hello definidos en el archivo de definición de servicio de Hola y especifica Hola número de instancias toorun para cada rol. Este archivo se puede actualizar mientras el servicio en la nube se ejecuta en Azure.

Hello Azure Tools para Microsoft Visual Studio proporciona páginas de propiedades que puede usar los valores de configuración de tooset almacenados en estos archivos. tooaccess Hola páginas de propiedades, haga doble clic en la referencia de rol de hello bajo el proyecto de servicio de nube de Azure de hello en el Explorador de soluciones, o haga referencia del rol hello y elija **propiedades**, tal y como se muestra en la figura siguiente de Hola.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Para obtener información sobre Hola subyacente esquemas de definición de servicio de Hola y de archivos de configuración de servicio, vea hello [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398.aspx). Para obtener más información acerca de la configuración de servicio, consulte [cómo los servicios de nube tooConfigure](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Configuración de las propiedades de rol
páginas de propiedades de Hola para un rol web y un rol de trabajo son similares, aunque hay algunas diferencias, que se indican en las secciones siguientes de Hola.

De hello **Caching** página, puede configurar Hola servicios de caching de Azure.

### <a name="configuration-page"></a>Página Configuración
En hello **configuración** página, puede establecer estas propiedades:

**Instances**

Conjunto hello **instancia** contar propiedad toohello número de instancias de servicio de Hola se debe ejecutar para este rol.

Conjunto hello **tamaño de máquina virtual** propiedad demasiado**Extra pequeño**, **pequeño**, **medio**, **grande**, o **Extragrande**.  Para obtener más información, consulte [Tamaños de Cloud Services](cloud-services/cloud-services-sizes-specs.md).

**Acción de inicio** (solo para el rol web)

Establecer este toospecify de propiedad que Visual Studio debería iniciar un explorador web para los extremos de hello HTTP, extremos HTTPS de Hola o ambos al iniciar la depuración.

Hola opción de punto de conexión HTTPS solo está disponible si ya se ha definido un extremo HTTPS para el rol. Puede definir un extremo HTTPS en hello **extremos** página de propiedades.

Si ya ha agregado un extremo HTTPS, Hola opción de punto de conexión HTTPS está habilitada de forma predeterminada, y Visual Studio iniciará un explorador para este extremo al iniciar la depuración, además tooa explorador para el extremo HTTP. Da por supuesto que están habilitadas las dos opciones de inicio.

**Diagnóstico**

De forma predeterminada, se habilitan los diagnósticos para el rol Web de Hola. Hola proyecto de servicio de nube de Azure y cuenta de almacenamiento se establecen emulador de almacenamiento local de toouse Hola. Cuando esté listo toodeploy tooAzure, puede seleccionar el botón Generador de hello (**...** ) tooupdate Hola almacenamiento cuenta toouse almacenamiento de Azure en la nube de Hola. Puede transferir la cuenta de almacenamiento de toohello de datos de diagnóstico de Hola a petición o en intervalos programados automáticamente. Para más información sobre los diagnósticos de Azure, consulte [Habilitación de Diagnósticos en Azure Cloud Services y Azure Virtual Machines](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Página Configuración
En hello **configuración** página, puede agregar valores de configuración para el servicio. Los valores de configuración son pares nombre-valor. Código que se ejecuta en función de hello puede leer valores de hello de las opciones de configuración en tiempo de ejecución utilizando las clases proporcionadas por hello [biblioteca administrada de Azure](http://go.microsoft.com/fwlink?LinkID=171026). En concreto, Hola [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) método devuelve el valor de Hola de una opción de configuración con nombre en tiempo de ejecución.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Configurar una cuenta de almacenamiento de tooa de cadena de conexión
Una cadena de conexión es una opción de configuración que proporciona información de conexión y autenticación para el emulador de almacenamiento de Hola o de una cuenta de almacenamiento de Azure. Cada vez que el código debe tener acceso a los datos de servicios de almacenamiento de Azure, es decir, blob, cola o datos de la tabla: desde el código que se ejecuta en un rol, tendrá que toodefine es una cadena de conexión para esa cuenta de almacenamiento.

Una cadena de conexión que señala tooan cuenta de almacenamiento de Azure debe usar un formato específico. Para obtener información acerca de cómo toocreate las cadenas de conexión, consulte [configurar cadenas de conexión de almacenamiento de Azure](storage/common/storage-configure-connection-string.md).

Cuando está listo tootest su servicio con servicios de almacenamiento de Azure de hello, o cuando esté listo toodeploy su tooAzure de servicio de nube, se puede cambiar el valor de Hola de cualquier tooyour toopoint de cadenas de conexión cuenta de almacenamiento de Azure. Haga clic en (**...**), seleccione **Especificar credenciales de cuenta de almacenamiento**. Escriba la información de la cuenta, incluidos el nombre y la clave de acceso. Hola **cadena de conexión de cuenta de almacenamiento** cuadro de diálogo, también puede indicar si desea toouse Hola HTTPS puntos de conexión predeterminados (opción predeterminada de hello), puntos de conexión HTTP de hello predeterminados o extremos personalizados. Podría decidir extremos personalizados toouse si se ha registrado un nombre de dominio personalizado para su servicio, tal y como se describe en [configurar un nombre de dominio personalizado para los datos blob en una cuenta de almacenamiento de Azure](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Debe modificar el tooan toopoint de cadenas de conexión cuenta de almacenamiento de Azure antes de implementar el servicio. Errores toodo Esto puede hacer que su rol no toostart o toocycle a través de Hola inicializando, ocupado y deteniendo.
> 
> 

## <a name="endpoints-page"></a>Página Extremos
Un rol de trabajador puede tener un número indeterminado de extremos HTTP, HTTPS o TCP. Los puntos de conexión pueden ser extremos de entrada, que son clientes de tooexternal disponibles, o extremos internos, que son roles de tooother disponibles que se ejecutan en el servicio de Hola.

* clientes de toomake HTTP endpoint tooexternal disponibles y los exploradores Web, cambiar tooinput de tipo de extremo de Hola y especifique un nombre y un número de puerto público.
* toomake HTTPS clientes de endpoint tooexternal disponibles y los exploradores Web, cambie el tipo del extremo de hello demasiado**entrada**y especifique un nombre, un número de puerto público y un nombre de certificado de administración.
  
    Tenga en cuenta que para poder especificar un certificado de administración, debe definir el certificado de hello en hello **certificados** página de propiedades.
* toomake un punto de conexión disponible para el acceso interno a otros roles en el servicio de nube de hello, cambiar toointernal de tipo de extremo de Hola y especifique un nombre y los puertos privados posibles para este extremo.

## <a name="local-storage-page"></a>Pagina Almacenamiento local
Puede usar hello **almacenamiento Local** tooreserve de página de propiedad uno o más recursos de almacenamiento local para un rol. Un recurso de almacenamiento local es un directorio reservado en el sistema de archivos de Hola de hello máquina virtual de Azure en que se ejecute una instancia de un rol.

## <a name="certificates-page"></a>Página Certificados
En hello **certificados** página, puede asociar certificados a un rol. certificados de Hola que agregue pueden ser utilizado tooconfigure los extremos HTTPS de hello **extremos** página de propiedades.

Hola **certificados** página de propiedades agrega información sobre la configuración del servicio de tooyour de certificados. Tenga en cuenta que los certificados no se incluyen con el servicio; debe cargar los certificados por separado tooAzure a través de hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate un certificado con su rol, proporcione un nombre para el certificado de Hola. Usar este certificado de nombre toorefer toohello cuando configura un extremo HTTPS en hello **extremos** página de propiedades. A continuación, especifique si el almacén de certificados de hello es **equipo Local** o **usuario actual** y el nombre de hello del almacén de Hola. Por último, especifique la huella digital del certificado de Hola. Si certificado hello es Hola personal actual (mi) almacén, puede escribir huella digital del certificado de hello mediante la selección de certificado de hello en una lista rellenada. Si se encuentra en cualquier otra ubicación, escriba valor de huella digital de Hola a mano.

Cuando se agrega un certificado del almacén de certificados de hello, cualquier certificado intermedio se agrega automáticamente toohello configuración. Estos certificados intermedios también se deben cargar tooAzure en orden toocorrectly configurar el servicio para SSL.

Cualquier certificado de administración que asocie a su servicio sólo aplica tooyour servicio cuando se está ejecutando en la nube de Hola. Cuando el servicio se ejecuta en el entorno de desarrollo local hello, usa un certificado estándar administrado por el emulador de proceso de Hola.

## <a name="configuring-hello-azure-cloud-service-project"></a>Configuración de proyecto de servicio de nube de Azure Hola
configuración de tooconfigure que se aplica el proyecto de servicio de nube de Azure completo tooan, primero abra menú contextual de Hola para ese nodo de proyecto y, a continuación, elija Propiedades tooopen sus páginas de propiedades. Hello en la tabla siguiente muestra las páginas de propiedades.

| Página de propiedades | Description |
| --- | --- |
| Application |Desde esta página, puede mostrar información acerca de la versión de Hola de Azure Tools que usa este proyecto de servicio de nube y puede actualizar la versión actual de toohello de herramientas de Hola. |
| Eventos de compilación |Desde esta página, puede establecer los eventos anteriores y posteriores a la compilación. |
| Desarrollo |Desde esta página, puede especificar las instrucciones de configuración de compilación y las condiciones de hello en la que se ejecutan los eventos posteriores a la compilación. |
| Web |Desde esta página, puede configurar opciones relacionadas con el servidor web de toohello. |

