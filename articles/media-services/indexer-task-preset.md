---
title: Valores predefinidos de tarea para Azure Media Indexer
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
ms.openlocfilehash: ae6c4da189cd6637b4e1fa9274473b62f6664e51
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Valores predefinidos de tarea para Azure Media Indexer

Azure Media Indexer es un procesador de multimedia que sirve para realizar las siguientes tareas: hacer posible la búsqueda de archivos multimedia y contenido, generar pistas de subtítulos y palabras clave, e indexar archivos de recursos que forman parte del recurso.

En este tema se describe el valor predefinido de tarea necesario para pasar al trabajo de indexación. Para un ejemplo completo, consulte [Indexación de archivos multimedia con Azure Media Indexer](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>XML de configuración de Azure Media Indexer

En la tabla siguiente se explican los elementos y los atributos de la configuración de XML.

|Nombre|Necesario|Descripción|
|---|---|---|
|Entrada|true|Archivos de recursos que desea indexar.<br/>Azure Media Indexer es compatible con los siguientes formatos de archivo multimedia: MP4, MOV, WMV, MP3, M4A, WMA, AAC y WAV. <br/><br/>Puede especificar los nombres de archivo en los atributos **name** o **list** del elemento **input** (tal y como se muestra a continuación). Si no especifica qué archivo de recursos indexar, se seleccionará el principal. Si no hay ningún archivo de recurso principal establecido, se indexa el primer recurso de entrada.<br/><br/>Para especificar explícitamente el nombre de archivo de recurso, haga:<br/>```<input name="TestFile.wmv" />```<br/><br/>También puede indexar varios archivos de recursos al mismo tiempo (hasta 10). Para ello, siga estos pasos:<br/>- Cree un archivo de texto (archivo de manifiesto) y asígnele una extensión .lst.<br/>- Agregue una lista de todos los nombres de archivos de recursos en el recurso de entrada a este archivo de manifiesto.<br/>- Agregue (cargue) el archivo de manifiesto al recurso.<br/>- Especifique el nombre del archivo de manifiesto en el atributo list de la entrada.<br/>```<input list="input.lst">```<br/><br/>**Nota**: Si agrega más de 10 archivos al archivo de manifiesto, el trabajo de indexación producirá un error con el código 2006.|
|metadata|false|Metadatos de los archivos de recursos especificados.<br/>```<metadata key="..." value="..." />```<br/><br/>Puede proporcionar valores para claves predefinidas. <br/><br/>Actualmente se admiten las siguientes claves:<br/><br/>**title** y **description**: se usan para actualizar el modelo de lenguaje y así mejorar la precisión del reconocimiento de voz.<br/>```<metadata key="title" value="[Title of the media file]" /><metadata key="description" value="[Description of the media file]" />```<br/><br/>**username** y **password**: se usan para la autenticación al descargar archivos de internet mediante http o https.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Los valores de username y password se aplican a todas las direcciones URL de los elementos multimedia del manifiesto de entrada.|
|features<br/><br/>Agregado en la versión 1.2. Actualmente solo se admite la característica de reconocimiento de voz ("ASR").|false|La característica de reconocimiento de voz tiene las siguientes claves de configuración:<br/><br/>Language:<br/>- Lenguaje natural que se reconocerá en el archivo multimedia.<br/>- Inglés, español.<br/><br/>CaptionFormats:<br/>- Lista con separación por punto y coma de los formatos de subtítulos de salida preferidos (si existen).<br/>- ttml; sami; webvtt.<br/><br/><br/>GenerateAIB:<br/>- Marca booleana que especifica si es o no un archivo AIB necesario (para su uso con SQL Server y el Indexer IFilter del cliente). Para más información, consulte el artículo sobre el uso de archivos AIB con Azure Media Indexer y SQL Server.<br/>- True; False.<br/><br/>GenerateKeywords:<br/>- Marca booleana que especifica si se requiere un archivo XML de palabras clave o no.<br/>- True; False.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Ejemplo de XML de configuración de Azure Media Indexer

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of the media file]" />  
    <metadata key="description" value="[Description of the media file]" />  
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

