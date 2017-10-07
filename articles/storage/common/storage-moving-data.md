---
title: aaaMoving grandes cantidades de datos de almacenamiento en nube de Azure | Documentos de Microsoft
description: "Información general de hello distintos métodos para mover tooand de datos del almacenamiento de Azure."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 7c8ec9d99cbd48042b8146130c8827f9f25c024d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Mover datos tooand desde el almacenamiento de Azure
Si desea que los datos tooAzure almacenamiento de toomove local (o viceversa), hay una gran variedad de formas toodo esto. enfoque de Hola que funciona mejor para usted dependerá de su escenario. Este artículo ofrece una breve descripción de diferentes escenarios y ofertas adecuadas para cada uno.

## <a name="building-applications"></a>Creación de aplicaciones
Si va a compilar una aplicación, desarrollo de soluciones con la API de REST de Hola o uno de nuestras muchas bibliotecas de cliente es un tooand de datos de manera estupenda toomove desde el almacenamiento de Azure.

Almacenamiento de Azure proporciona bibliotecas de cliente enriquecidas para .NET, iOS, Java, Android, Plataforma universal de Windows (UWP), Xamarin, C++, Node.JS, PHP, Ruby y Python. bibliotecas de cliente de Hello ofrecen capacidades avanzadas como la lógica de reintento, registro y cargas en paralelo. También puede desarrollar directamente contra Hola API de REST, que se puede llamar mediante cualquier lenguaje que realiza las solicitudes HTTP/HTTPS.

Vea [Introducción al almacenamiento de blobs de Azure](../blobs/storage-dotnet-how-to-use-blobs.md) toolearn más.

Además, también le ofrecemos hello [biblioteca de movimiento de datos de almacenamiento de Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) que es una biblioteca que se ha diseñado para la copia de alto rendimiento de tooand de datos de Azure. Consulte tooour biblioteca de movimiento de datos [documentación](https://github.com/Azure/azure-storage-net-data-movement) toolearn más. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Visualización o interacción rápida con los datos
Si desea un tooview fácilmente los datos de almacenamiento de Azure ejerciendo también tooupload de capacidad de Hola y descargar los datos, considere la posibilidad de usar un explorador de almacenamiento de Azure.

Visite nuestra lista de [exploradores de almacenamiento de Azure](../storage-explorers.md) toolearn más.

## <a name="system-administration"></a>Administración del sistema
Si se requieren o se está más familiarizado con una utilidad de línea de comandos (por ejemplo, los administradores del sistema), aquí tiene algunas opciones para tooconsider:

### <a name="azcopy"></a>AzCopy
AzCopy es una utilidad de línea de comandos de Windows diseñada para la copia de alto rendimiento de tooand de datos del almacenamiento de Azure. También puede copiar datos de blobs en la cuenta de almacenamiento o entre distintas cuentas de este tipo.

Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md) toolearn más.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell es un módulo que proporciona cmdlets para administrar servicios en Azure. Se trata de un shell de línea de comandos basado en tareas y un lenguaje de scripts especialmente diseñados para administración del sistema.

Vea [uso de PowerShell de Azure con el almacenamiento de Azure](storage-powershell-guide-full.md) toolearn más.

### <a name="azure-cli"></a>CLI de Azure
CLI de Azure proporciona un conjunto de comandos de código abierto y multiplataforma para trabajar con los servicios de Azure. CLI de Azure está disponible en Windows, OSX y Linux.

Vea [Using Hola CLI de Azure con el almacenamiento de Azure](../storage-azure-cli.md) toolearn más.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Movimiento de grandes cantidades de datos con una red lenta
Uno de los mayores desafíos de hello asociados con el movimiento de grandes cantidades de datos es el tiempo de transferencia de Hola. Si desea tooget datos desde almacenamiento de Azure sin preocuparse por los costos de redes o escribir código, importación y exportación de Azure es una solución adecuada.

Vea [importación/exportación de Azure](../storage-import-export-service.md) toolearn más.

## <a name="backing-up-your-data"></a>Realización de una copia de seguridad de los datos
Si simplemente necesita toobackup el almacenamiento de datos tooAzure, copia de seguridad de Azure es Hola forma toogo. Se trata de una solución eficaz para la copia de seguridad de los datos locales y máquinas virtuales de Azure.

Vea [copia de seguridad de Azure](../../backup/backup-introduction-to-azure-backup.md) toolearn más.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>Obtener acceso a los datos locales y de nube de Hola
Si necesita una solución para tener acceso a los datos locales y de nube de hello, debe plantearse usar solución de almacenamiento en la nube híbrida de Azure, StorSimple. Esta solución consta de un dispositivo físico de StorSimple que almacena de manera inteligente los datos usados con más frecuencia en las unidades SSD, los datos menos usados en unidades de disco duro y los datos inactivos, de copia de seguridad o de archivado en Almacenamiento de Azure.

Vea [StorSimple](../../storsimple/storsimple-overview.md) toolearn más.

## <a name="recovering-your-data"></a>Recuperación de los datos
Si tiene aplicaciones y cargas de trabajo local, necesitará una solución que permita su toocontinue business ejecutando en caso de hello de un desastre. Azure Site Recovery controla la replicación, la conmutación por error y la recuperación de máquinas virtuales y servidores físicos. Los datos replicados se almacenan en el almacenamiento de Azure, permitiéndole tooeliminate Hola necesario para un centro de datos en el sitio secundario.

Vea [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) toolearn más.
### <a name="moving-data-faq"></a>Preguntas más frecuentes sobre movimiento de datos:
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>¿Puedo migrar discos duros virtuales de tooanother de una región sin necesidad de copiar?
Hello solo forma toocopy discos duros virtuales entre región es datos de hello toocopy entre cuentas de almacenamiento en cada región. Puede utilizar AZCopy para ello. Ver los datos de transferencia con hello la utilidad de línea de comandos de AzCopy toolearn más. Para grandes cantidades de datos, también puede importar/exportar de Azure. Vea [importación/exportación de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn más.
