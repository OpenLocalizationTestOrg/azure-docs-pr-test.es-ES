---
title: "Hola aaaTroubleshooting herramienta de importación y exportación de Azure | Documentos de Microsoft"
description: "Información sobre algunos de los problemas comunes de hello aparece cuando se usa la herramienta de importación y exportación de Azure de Hola y cómo toohandle ellos."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Solución de problemas de hello herramienta de importación y exportación de Azure
Hola herramienta de importación y exportación de Microsoft Azure devuelve mensajes de error si encuentra problemas. En este tema se enumeran algunos problemas comunes con los que los usuarios se pueden encontrar.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Se produce un error en una sesión de copia, ¿qué debo hacer?  
 Cuando se produce un error en una sesión de copia, tiene dos opciones:  
  
 Si el error de hello es recuperable, por ejemplo, si el recurso compartido de red de hello estaba sin conexión para una breve período y ahora es nuevo en línea, puede reanudar la sesión de copia de Hola. Si Hola error no es recuperable, por ejemplo, si ha especificado el directorio de archivos de origen incorrecto de hello en parámetros de línea de comandos de hello, deberá sesión de copia de tooabort Hola. Vea [Preparación de unidades de disco duro para un trabajo de importación](../storage-import-export-tool-preparing-hard-drives-import-v1.md) para más información sobre cómo reanudar y anular sesiones de copia.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>No puedo reanudar o anular una sesión de copia.  
 Si es de sesión de copia de Hola Hola primera sesión de copia de una unidad, debería indicar el mensaje de error de Hola: "hello primera sesión de copia se no se puede reanudar o anulado." En este caso, puede eliminar el archivo de diario anterior de Hola y vuelva a ejecutar el comando Hola.  
  
 Si una sesión de copia no es hello primera de ellas para una unidad, siempre puede reanudar o anulado.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>He perdido el archivo de diario de hello, ¿todavía puedo crear trabajo de hello?  
 archivo de diario de Hola para una unidad de disco contiene Hola toda la información de copia de unidad de datos toothis, y es necesario tooadd más unidad de archivos de toohello y será toocreate usa un trabajo de importación. Si el archivo de diario de Hola se pierde, tendrá tooredo todas las sesiones de copia de Hola para unidad de Hola.  
  
## <a name="next-steps"></a>Pasos siguientes
 
* [Configurar la herramienta de importación y exportación de azure Hola](../storage-import-export-tool-setup-v1.md)   
* [Preparación de unidades de disco duro para un trabajo de importación](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisión del estado del trabajo con archivos de registro de copia](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparación de un trabajo de importación](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Reparación de un trabajo de exportación](../storage-import-export-tool-repairing-an-export-job-v1.md)
