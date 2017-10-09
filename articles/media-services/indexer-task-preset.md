---
title: aaaTask preestablecido para Azure Media Indexer
description: "En este tema se ofrece información general sobre los valores predefinidos de tarea para Azure Media Indexer."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Valores predefinidos de tarea para Azure Media Indexer

Azure Media Indexer es un procesador multimedia que usas hello tooperform siguiente las tareas: hacer posible la búsqueda de archivos multimedia y el contenido, generar pistas de subtítulos y palabras clave, indexar archivos de recursos que forman parte del recurso.

Este tema describe Hola predefinidos de tarea que debe tooyour toopass indización de trabajo. Para un ejemplo completo, consulte [Indexación de archivos multimedia con Azure Media Indexer](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>XML de configuración de Azure Media Indexer

Hello siguiente tabla explica elementos y atributos del XML de configuración de Hola.

|Nombre|Necesario|Descripción|
|---|---|---|
|Entrada|true|Archivos de recurso que desea tooindex.<br/>Azure Media Indexer es compatible con hello siguientes formatos de archivo multimedia: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>Puede especificar el nombre de archivo (s) de Hola Hola **nombre** o **lista** atributo de hello **entrada** elemento (tal y como se muestra a continuación). Si no especifica qué tooindex del archivo de activos, se seleccionará el archivo principal de Hola. Si se establece ningún archivo de recurso principal, se indiza archivo primera hello en el recurso de entrada de Hola.<br/><br/>tooexplicitly especificar nombre de archivo de activos de hello, realice:<br/>```<input name="TestFile.wmv" />```<br/><br/>También puede indizar varios archivos de recursos a la vez (seguridad de los archivos de too10). toodo esto:<br/>- Cree un archivo de texto (archivo de manifiesto) y asígnele una extensión .lst.<br/>-Agregar una lista de todos los nombres de archivo de activos de hello en el archivo de manifiesto de recurso de entrada toothis.<br/>-Agregar (cargar) thanifest archivo toohello activo.<br/>-Especifique el nombre de Hola Hola del archivo de manifiesto en el atributo de la lista de la entrada de Hola.<br/>```<input list="input.lst">```<br/><br/>**Nota:** si agrega más de 10 archivos de archivo de manifiesto toohello, trabajo de indexación de Hola se producirá un error con código de error de hello 2006.|
|metadata|false|Metadatos de hello especifican archivos de recurso.<br/>```<metadata key="..." value="..." />```<br/><br/>Puede proporcionar valores para claves predefinidas. <br/><br/>Actualmente, se admite Hola siguiendo las claves:<br/><br/>**título** y **descripción** -utiliza la precisión del reconocimiento de tooupdate Hola lenguaje modelo tooimprove voz.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**username** y **password**: se usan para la autenticación al descargar archivos de internet mediante http o https.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Hola nombre de usuario y las direcciones URL de tooall multimedia en el manifiesto de entrada de Hola aplican los valores de contraseña.|
|features<br/><br/>Agregado en la versión 1.2. Actualmente, la característica de hello solo admitido es el reconocimiento de voz ("ASR").|false|característica de reconocimiento de voz de Hello tiene Hola después de claves de configuración:<br/><br/>Language:<br/>-Hola toobe de lenguaje natural que se reconocen en el archivo multimedia de hello.<br/>- Inglés, español.<br/><br/>CaptionFormats:<br/>-una lista separada por punto y coma de hello deseado formatos de salida de título (si existe)<br/>- ttml; sami; webvtt.<br/><br/><br/>GenerateAIB:<br/>-Una marca booleana que especifica si un archivo AIB se requiere (para su uso con clientes de SQL Server y Hola IFilter del indexador). Para más información, consulte el artículo sobre el uso de archivos AIB con Azure Media Indexer y SQL Server.<br/>- True; False.<br/><br/>GenerateKeywords:<br/>- Marca booleana que especifica si se requiere un archivo XML de palabras clave o no.<br/>- True; False.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Ejemplo de XML de configuración de Azure Media Indexer

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Pasos siguientes

Consulte [Indexación de archivos multimedia con Azure Media Indexer](media-services-index-content.md).

