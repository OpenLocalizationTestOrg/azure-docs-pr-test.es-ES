---
title: rendimiento de aaaImprove al comprimir los archivos de red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de la transferencia de archivos de tooimprove velocidad y aumenta el rendimiento de carga de la página mediante la compresión de los archivos de red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Mejora del rendimiento comprimiendo archivos en la red CDN de Azure
La compresión es la velocidad de transferencia de archivos de tooimprove método sencillo y eficaz y aumento del rendimiento de carga de página al reducir el tamaño del archivo antes de que se envía desde el servidor de Hola. Este método reduce los costos de ancho de banda y proporciona una mayor capacidad de respuesta para los usuarios.

Hay dos maneras de compresión de tooenable:

* Puede habilitar la compresión en el servidor de origen, en cuyo caso hello CDN pasa a través de hello archivos comprimidos y entrega archivos comprimidos tooclients que las solicitan.
* Puede habilitar la compresión directamente en servidores perimetrales CDN, en la que comprime CDN Hola mayúsculas Hola archivos y servir a los usuarios tooend, incluso si no se comprimen mediante el servidor de origen de Hola.

> [!IMPORTANT]
> Cambios de configuración de red CDN tienen algunas toopropagate tiempo a través de la red de Hola.  Para los perfiles de la <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completa en menos de un minuto.  Para los perfiles de la <b>red CDN de Azure de Verizon</b> , normalmente verá que los cambios se aplican en un período de 90 minutos.  Si se trata de hello primera vez que se ha establecido la compresión para el punto de conexión, considere la posibilidad de espera 1 y 2 horas toobe seguro de los valores de compresión de hello propagaron POP toohello antes de la solución de problemas
> 
> 

## <a name="enabling-compression"></a>Habilitar la compresión
> [!NOTE]
> proporcionan Hello niveles Standard y Premium CDN Hola la misma funcionalidad de compresión, pero difiere de hello interfaz de usuario.  Para obtener más información acerca de las diferencias de hello entre niveles Standard y Premium CDN, vea [información general sobre la red CDN de Azure](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Nivel Standard
> [!NOTE]
> En esta sección se aplica demasiado**estándar de red CDN de Azure de Verizon** y **estándar de red CDN de Azure de Akamai** perfiles.
> 
> 

1. En la página de perfil CDN Hola, haga clic en extremo de red CDN Hola desea toomanage.
   
    ![Puntos de conexión de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    Abre la página de punto de conexión de red CDN Hola.
2. Haga clic en hello **configurar** botón.
   
    ![Botón de administración de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    Abre la página de configuración de red CDN Hola.
3. Active la **Compresión**.
   
    ![Opciones de compresión de red CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. Utilizar tipos de valor predeterminado de hello, o modificar lista de hello quitando o agregando los tipos de archivo.
   
   > [!TIP]
   > Mientras sea posible, se recomienda no tooapply compresión toocompressed formatos, como ZIP, MP3, MP4, JPG, etcetera.
   > 
   > 
5. Después de realizar los cambios, haga clic en hello **guardar** botón.

### <a name="premium-tier"></a>Nivel Premium
> [!NOTE]
> En esta sección se aplica demasiado**Premium de CDN de Azure de Verizon** perfiles.
> 
> 

1. En la página de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Mantenga el mouse sobre hello **HTTP grandes** ficha y, a continuación, mantenga el mouse sobre hello **configuración de la caché** ventana flotante.  Haga clic en **Compresión**.

    ![Selección de compresión de archivos](./media/cdn-file-compression/cdn-compress-select.png)
   
    Se muestran las opciones de compresión.
   
    ![Compresión de archivos](./media/cdn-file-compression/cdn-compress-files.png)
3. Habilitar la compresión, haga clic en hello **compresión habilitada** botón de radio.  Escriba los tipos MIME Hola indeterminado toocompress como una lista delimitada por comas (sin espacios) en hello **tipos de archivo** cuadro de texto.
   
   > [!TIP]
   > Mientras sea posible, se recomienda no tooapply compresión toocompressed formatos, como ZIP, MP3, MP4, JPG, etcetera. 
   > 
   > 
4. Después de realizar los cambios, haga clic en hello **actualización** botón.

## <a name="compression-rules"></a>Reglas de compresión
Estas tablas describen el comportamiento de la compresión CDN de Azure para cada escenario.

> [!IMPORTANT]
> En el caso de la **red CDN de Azure de Verizon** (estándar y premium), solo se comprimen determinados archivos válidos.  un archivo de toobe apta para la compresión, debe:
> 
> * Debe tener más de 128 bytes.
> * Debe tener menos de 1 MB.
> 
> En el caso de la **red CDN de Azure de Akamai**, todos los archivos son válidos para la compresión.
> 
> Para todos los productos de la red CDN de Azure, un archivo debe tener un tipo MIME [configurado para compresión](#enabling-compression).
> 
> Los perfiles de **CDN de Azure de Verizon** (Standard y Premium) admiten la codificación **gzip** (GNU zip), **deflate**, **bzip2** o **br** (Brotli). Para la codificación Brotli, compresión de Hola se realiza solo en el perímetro de Hola. Hola/explorador del cliente debe enviar la solicitud de Hola de codificación Brotli y activos comprimido Hola deben se han comprimido en el lado de origen de hello en primer lugar. 
>
>Los perfiles de **CDN de Azure de Akamai** solo admiten la codificación **gzip**.
> 
> **Azure CDN de Akamai** puntos de conexión siempre solicitarán **gzip** archivos de origen de hello, independientemente de la solicitud de cliente hello codificados. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>La compresión está deshabilitada o el archivo no es elegible para la compresión
| Formato solicitado por el cliente (mediante el encabezado Accept-Encoding) | Formato de archivo almacenado en caché | Cliente de red CDN respuesta toohello | Notas |
| --- | --- | --- | --- |
| Comprimidos |Comprimidos |Comprimidos | |
| Comprimidos |Sin comprimir |Sin comprimir | |
| Comprimidos |No almacenado en caché |Comprimidos o sin comprimir |Depende de la respuesta de origen |
| Sin comprimir |Comprimidos |Sin comprimir | |
| Sin comprimir |Sin comprimir |Sin comprimir | |
| Sin comprimir |No almacenado en caché |Sin comprimir | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>La compresión está habilitada y el archivo es elegible para la compresión
| Formato solicitado por el cliente (mediante el encabezado Accept-Encoding) | Formato de archivo almacenado en caché | Cliente de red CDN respuesta toohello | Notas |
| --- | --- | --- | --- |
| Comprimidos |Comprimidos |Comprimidos |La red CDN transcodifica entre los formatos admitidos |
| Comprimidos |Sin comprimir |Comprimidos |La red CDN realiza la compresión |
| Comprimidos |No almacenado en caché |Comprimidos |La red CDN realiza la compresión si el origen se devuelve sin comprimir.  **Red CDN de Azure de Verizon** pasadas Hola archivo sin comprimir en la primera solicitud de hello y, a continuación, comprime y memorias caché Hola archivo para las solicitudes posteriores.  Los archivos con el encabezado `Cache-Control: no-cache` nunca se comprimirán. |
| Sin comprimir |Comprimidos |Sin comprimir |La red CDN realiza la descompresión |
| Sin comprimir |Sin comprimir |Sin comprimir | |
| Sin comprimir |No almacenado en caché |Sin comprimir | |

## <a name="media-services-cdn-compression"></a>Compresión de red CDN de servicios multimedia
Media Services CDN ha habilitado los extremos de streaming, está habilitada la compresión predeterminada para los siguientes tipos de contenido de hello: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, aplicación/f4m + xml. No puede habilitar o deshabilitar la compresión de hello mencionados tipos mediante Hola portal de Azure.  

## <a name="see-also"></a>Otras referencias
* [Solución de problemas de compresión de archivos de red CDN](cdn-troubleshoot-compression.md)    

