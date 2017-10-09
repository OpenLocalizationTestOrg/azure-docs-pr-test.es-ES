---
title: aaaMove tooand de datos desde almacenamiento de blobs con el Explorador de almacenamiento de Azure | Documentos de Microsoft
description: Mover datos tooand de almacenamiento de blobs de Azure mediante el Explorador de almacenamiento de Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Mover datos tooand de almacenamiento de blobs de Azure mediante el Explorador de almacenamiento de Azure
Explorador de almacenamiento de Azure es una herramienta gratuita de Microsoft que le permite toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux. Este tema se describe cómo toouse, almacenamiento de blobs de datos tooupload y descarga de Azure. herramienta de Hello puede descargarse desde [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si está usando la máquina virtual que se configuró con secuencias de comandos de hello proporcionadas por [máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), a continuación, el Explorador de almacenamiento de Azure ya está instalado en hello VM.
> 
> [!NOTE]
> Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y [servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Este documento se da por supuesto que tiene una suscripción de Azure, una cuenta de almacenamiento y la clave de almacenamiento correspondiente de Hola para esa cuenta. Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta. 

* tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md). Asegúrese de una clave de acceso de hello Nota para la cuenta de almacenamiento según sea necesario a esta cuenta de toohello tooconnect clave con la herramienta del explorador de almacenamiento de Azure Hola.
* herramienta del explorador de almacenamiento de Azure Hola puede descargarse desde [Microsoft Azure Storage Explorer](http://storageexplorer.com/). Acepte los valores predeterminados de Hola durante la instalación.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Usar el Explorador de almacenamiento de Azure
Hola siguiente documento pasos cómo tooupload/descargar datos mediante el Explorador de almacenamiento de Azure. 

1. Inicie Explorador de almacenamiento de Microsoft Azure.
2. toobring seguridad hello **iniciar sesión en la cuenta de tooyour...**  asistente, seleccione **configuración de la cuenta de Azure** icono, a continuación, **agregar una cuenta** y escriba las credenciales. ![Agregar una cuenta de Azure Storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring seguridad hello **conectar tooAzure almacenamiento** Hola asistente, seleccione **conectar almacenamiento tooAzure** icono. ![Conectar almacenamiento tooAzure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Escriba la clave de acceso de Hola de su cuenta de almacenamiento de Azure en hello **conectar tooAzure almacenamiento** asistente y, a continuación, **siguiente**. ![Conectar almacenamiento tooAzure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Escriba el nombre de la cuenta de almacenamiento en hello **nombre-cuenta** cuadro y, a continuación, seleccione **siguiente**. ![Adjuntar almacenamiento externo](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. cuenta de almacenamiento de Hello agregada debe aparecer ahora. toocreate un contenedor de blobs en una cuenta de almacenamiento, haga clic en hello **contenedores de blobs** nodo en esa cuenta, seleccione **crear contenedor de blobs**y escriba un nombre.
7. contenedor de tooupload datos tooa, seleccione Hola Hola de contenedor y haga clic en de destino **cargar** botón.![ Cuentas de almacenamiento](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Haga clic en hello **...**  toohello derecha de hello **archivos** , seleccione uno o varios tooupload de archivos de sistema de archivos de Hola y haga clic en **cargar** toobegin cargar archivos de Hola.![ Cargar archivos](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. datos de toodownload, seleccionando Hola blob en toodownload contenedor correspondiente de Hola y haga clic en **descargar**. ![Descargar archivos](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

