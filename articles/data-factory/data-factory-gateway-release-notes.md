---
title: notas de la aaaRelease de Data Management Gateway | Documentos de Microsoft
description: "Notas de la versión de Data Management Gateway"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Notas de la versión de Data Management Gateway
Uno de los desafíos de hello para la integración de datos modernas es toomove datos tooand desde toocloud local. Factoría de datos hace que esta integración con Data Management Gateway, que es un agente que puede instalar el movimiento de datos local tooenable híbrida.

Vea Hola siguientes artículos para obtener información detallada acerca de la puerta de enlace de datos de administración y cómo toouse:

*  [Data Management Gateway](data-factory-data-management-gateway.md)
*  [Movimiento de datos entre una ubicación local y la nube mediante Factoría de datos de Azure](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>VERSIÓN ACTUAL (2.10.6347.7)

### <a name="enhancements-"></a>Mejoras-
- Puede agregar bus de servicio de toowhitelist de las entradas DNS en lugar de crear listas blancas con todas las direcciones IP de Azure desde el servidor de seguridad (si es necesario). Puede encontrar la entrada DNS correspondiente en Azure Portal (Data Factory -> "Crear e implementar" -> "Puertas de enlace" -> "serviceUrls" (en JSON)
- El conector HDFS admite ahora certificados públicos autofirmados para poder omitir la validación de SSL.
- Corregido: Problema con la puerta de enlace sin conexión durante la actualización (vence tooclock sesgo)



## <a name="earlier-versions"></a>Versiones anteriores

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Mejoras-
-   Puede agregar las entradas DNS toowhitelist Bus de servicio en lugar de crear listas blancas con todas las direcciones IP de Azure desde el servidor de seguridad (si es necesario). Más detalles aquí.
-   Ahora puede copiar datos de un blob en bloques solo seguridad too4.75 TB, que es el tamaño de hello max compatible de blob en bloques. (el límite anterior era 195 GB).
-   Problema solucionado: memoria agotada al descomprimir varios archivos pequeños durante la actividad de copia.
-   Problema corregido: Índice fuera del problema de intervalo mientras se copiaba del tooan de base de datos de documentos en SQL Server local con la característica de idempotencia.
-   Problema solucionado: el script de limpieza SQL no funciona en la instancia de SQL Server local desde el Asistente para copia.
-   Problema corregido: Nombre de la columna con espacio final hello no funciona en la actividad de copia.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Mejoras-
- Problema solucionado: falta de credenciales durante el reinicio de máquina de puerta de enlace.
- Solucionado: problema de registro durante la restauración de la puerta de enlace mediante un archivo de copia de seguridad.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Mejoras-
- Problema solucionado: lectura incorrecta de valor NULL decimal desde Oracle como origen.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>Novedades
- Los clientes pueden proporcionar comentarios en la experiencia de registro de la puerta de enlace.
- Nuevo formato de compresión compatible: ZIP (Deflate).

### <a name="enhancements-"></a>Mejoras-
- Mejora del rendimiento del origen de HDFS y el receptor de Oracle.
- Corrección de errores de la capacidad de procesamiento en paralelo y la actualización automática de la puerta de enlace.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Mejoras
- Mejorada y más sólida puerta de enlace registro experiencia: ahora puede realizar el seguimiento del estado del progreso durante el proceso de registro de puerta de enlace de hello, lo que permite el registro de hello experimentar mayor capacidad de respuesta.
- Mejora de la puerta de enlace restaurar proceso - que todavía puede recuperar la puerta de enlace incluso si no tiene archivos de copia de seguridad de puerta de enlace de hello con esta actualización. Esto requeriría tooreset las credenciales de servicio vinculado en el Portal.
- Corrección de errores.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>Novedades

- Ahora puede almacenar localmente las credenciales de origen de datos. Hola credenciales se cifran. las credenciales del origen de datos de Hola se pueden recuperar y restauran con el archivo de copia de seguridad de hello que se pueden exportar desde Hola existente de la puerta de enlace local en todos los.

### <a name="enhancements-"></a>Mejoras-

- Experiencia de registro de puerta de enlace mejorada y más eficaz.
- Compatibilidad con detección automática de la configuración de QuoteChar texto sin formato en el Asistente para copiar y mejorar Hola precisión en la detección de formato general.

## <a name="2361002"></a>2.3.6100.2

- Compatibilidad con la detección automática de firstRowAsHeader y SkipLineCount en el Asistente para copia para archivos de texto en el sistema de archivos local y HDFS.
- Mejorar la estabilidad de Hola de conexión de red entre la puerta de enlace y el Bus de servicio
- Unas pocas correcciones de errores


## <a name="2260721"></a>2.2.6072.1

*  Admite la configuración de proxy HTTP para el uso de la puerta de enlace de Hola Hola puerta de enlace de Configuration Manager. Si está configurado, se accede a Blob de Azure, Tabla de Azure, Azure Data Lake y DocumentDB a través del proxy HTTP.
*  Encabezado de admite el control de TextFormat cuando se copian datos desde / tooAzure Blob, almacén de Azure Data Lake, sistema de archivos local y HDFS local.
*  Permite copiar los datos de Blob de anexar y Blob en páginas junto con hello ya admite Blob en bloques.
*  Presenta un nuevo estado de puerta de enlace **en línea (limitado)**, lo que indica que esa funcionalidad principal de Hola de puerta de enlace de hello funciona excepto la compatibilidad con la operación interactiva de hello para el Asistente para copiar.
*  Mejora la solidez del saludo del registro de puerta de enlace con la clave de registro.

## <a name="216040"></a>2.1.6040.

*  Controlador de DB2 se incluye en el paquete de instalación de puerta de enlace de hello ahora. No es necesario tooinstall lo por separado.
*  Controlador de DB2 ahora es compatible con z/OS y DB2 para (AS / 400) junto con plataformas de hello ya compatibles (Linux, Unix y Windows).
*  Admite el uso de Azure Cosmos DB como origen o destino para almacenes de datos locales
*  Permite la copia de almacenamiento de blobs de/toocold/activos de datos junto con hello ya admite la cuenta de almacenamiento general.
*  Le permite tooconnect tooon local SQL Server a través de puerta de enlace con privilegios de inicio de sesión remoto.  

## <a name="2060131"></a>2.0.6013.1

*  Puede seleccionar toobe de lenguaje o la referencia cultural de hello usa una puerta de enlace durante la instalación manual.

*  Cuando la puerta de enlace no funciona según lo previsto, puede elegir toosend registros de puerta de enlace de últimos siete días tooMicrosoft toofacilitate solución de problemas de emisión de Hola. Si la puerta de enlace no está conectado toohello servicio en la nube, puede elegir toosave y almacene los registros de puerta de enlace.  

*  Mejoras de la interfaz de usuario del Administrador de configuración de puertas de enlace:

    *  Asegúrese de estado de la puerta de enlace más visible en la pestaña Inicio de Hola.

    *  Controles reorganizados y simplificados.

    *  Puede copiar los datos de un almacenamiento con hello [herramienta de vista previa de la copia sin código](data-factory-copy-data-wizard-tutorial.md). Para obtener más información general sobre esta característica consulte [Copias almacenadas provisionalmente](data-factory-copy-activity-performance.md#staged-copy) .
*  Puede utilizar Data Management Gateway tooingress directamente los datos de una base de datos de SQL Server local en aprendizaje automático de Azure.

*  Mejoras en el rendimiento

    * Se ha mejorado el rendimiento al visualizar los esquemas y la vista previa en SQL Server mediante la herramienta de vista previa de copia sin código.

## <a name="11259531"></a>1.12.5953.1

*  Corrección de errores

## <a name="11159181"></a>1.11.5918.1

*  Se ha aumentado el tamaño máximo del registro de eventos de puerta de enlace de Hola de 1 MB de too40 MB.

*  En caso de que se requiera un reinicio durante la actualización automática de la puerta de enlace, se muestra un cuadro de diálogo de advertencia. Puede elegir toorestart derecha, a continuación, o una versión posterior.

*  En caso de error en la actualización automática, el instalador de puerta de enlace volverá a intentar esta operación 3 veces al máximo.

*  Mejoras en el rendimiento

    * Rendimiento mejorado para la carga de tablas de gran tamaño desde el servidor local en un escenario de copia sin código.

*  Corrección de errores

## <a name="11058921"></a>1.10.5892.1

*  Mejoras en el rendimiento

*  Corrección de errores

## <a name="1958652"></a>1.9.5865.2

*  Funcionalidad de actualización automática sin intervención del usuario
*  Icono de bandeja de nuevo con indicadores de estado de la puerta de enlace
*  Capacidad demasiado "Actualizar ahora" desde el cliente de Hola
*  Hora de programación de actualización de capacidad tooset
*  Script de PowerShell para activar y desactivar la actualización automática
*  Compatibilidad con formato JSON  
*  Mejoras en el rendimiento
*  Corrección de errores

## <a name="1858221"></a>1.8.5822.1

*  Mejora de la solución de problemas
*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1757951"></a>1.7.5795.1

*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1757641"></a>1.7.5764.1

*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1657351"></a>1.6.5735.1

*  Compatibilidad origen y receptor HDFS locales
*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1656961"></a>1.6.5696.1

*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1656761"></a>1.6.5676.1

*  Compatibilidad con herramientas de diagnóstico de Administrador de configuración
*  Columnas de la tabla de soporte técnico para orígenes de datos tabulares de la Factoría de datos de Azure
*  Compatibilidad con SQL DW para Factoría de datos de Azure
*  Compatibilidad con Reclusive en BlobSource y FileSource para Factoría de datos de Azure
*  Compatibilidad con CopyBehavior - MergeFiles, PreserveHierarchy y FlattenHierarchy en BlobSink y FileSink con copia binaria para Data Factory de Azure
*  Compatibilidad con los informes de progreso de la actividad de copia para Factoría de datos de Azure
*  Compatibilidad con la validación de conectividad de origen de datos para Factoría de datos de Azure
*  Corrección de errores

### <a name="1656721"></a>1.6.5672.1

*  Compatibilidad con nombre de tabla de origen de datos ODBC para Factoría de datos de Azure
*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1656581"></a>1.6.5658.1

*  Compatibilidad con receptor de archivos para Factoría de datos de Azure
*  Compatibilidad con la conservación jerarquía en copia binaria para Factoría de datos de Azure
*  Compatibilidad con idempotencia de la actividad de copia para Factoría de datos de Azure
*  Corrección de errores

### <a name="1656401"></a>1.6.5640.1

*  Compatibilidad con tres orígenes de datos más para Factoría de datos de Azure (ODBC, OData y HDFS)
*  Compatibilidad con carácter de comillas en el analizador de archivos .csv para Factoría de datos de Azure
*  Compatibilidad con compresión (BZip2)
*  Corrección de errores

### <a name="1556121"></a>1.5.5612.1

*  Compatibilidad con cinco bases de datos relacionales para Data Factory de Azure (MySQL, PostgreSQL, DB2, Teradata y Sybase)
*  Compatibilidad de compresión (Gzip y Deflate)
*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1455491"></a>1.4.5549.1

*  Incorporación de compatibilidad de origen de datos Oracle para Factoría de datos de Azure
*  Mejoras en el rendimiento
*  Corrección de errores

### <a name="1454921"></a>1.4.5492.1

*  Binario unificado que admite los servicios Factoría de datos de Microsoft Azure y Office 365 Power BI
*  Refinar el proceso de interfaz de usuario de configuración y el registro de hello
*  Factoría de datos de Azure: compatibilidad de entrada y salida de Azure con origen de datos SQL Server

### <a name="1253031"></a>1.2.5303.1

*  Corregir toosupport de problema de tiempo de espera más conexiones que consumen muchos recursos de orígenes de datos.

### <a name="1155268"></a>1.1.5526.8

*  Requiere .NET Framework 4.5.1 como requisito previo durante la instalación.

### <a name="1051442"></a>1.0.5144.2

*  No hay cambios que afecten a los escenarios de Factoría de datos de Azure.
