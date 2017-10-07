---
title: aaaDisplaying contenido de Javadoc en Eclipse para hello paquete de bibliotecas de Azure para Java
description: "¿Cómo toodisplay Hola contenido de Javadoc Hola para bibliotecas de Azure en Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Mostrar el contenido de Javadoc en Eclipse para hello paquete de bibliotecas de Azure para Java
Hola contenido de Javadoc de hello bibliotecas de Azure para Java puede verse en el entorno Eclipse asociando hello toohello contenido de Javadoc bibliotecas de Azure para Java. Hello pasos siguientes muestran cómo toouse esta funcionalidad en Eclipse.

Este procedimiento se da por supuesto que ya ha agregado hello biblioteca de Azure para la ruta de acceso de compilación de Java tooyour.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay contenido de Javadoc en Eclipse para hello bibliotecas de Azure para Java
* En el Explorador de proyectos de Eclipse, en hello **hace referencia a bibliotecas** menú contextual abierto Hola Hola biblioteca de Azure para JAR de Java, en una sección del proyecto. Por ejemplo, **microsoft-Windows-api-0.1.0** (número de versión de Hola puede ser diferente, dependiendo de qué versión ha instalado).

* Haga clic en **Propiedades**.

* Dentro de hello **propiedades** cuadro de diálogo, en el panel izquierdo de hello, haga clic en **ubicación de Javadoc**. Hola **ubicación de Javadoc** se muestra el cuadro de diálogo.

* Puede especificar una **Javadoc URL** (URL de Javadoc) o un **Javadoc in archive** (Javadoc en archivo).

   * Si elige toospecify una **dirección URL de Javadoc**, utilice direcciones URL de hello como **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.

   * Si elige toouse **Javadoc en archivo**, puede especificar un archivo externo o un archivo de área de trabajo.

   Realice su elección y examine o valide según sea necesario. Hello en el ejemplo siguiente se asocia hello Azure Libraries for Java Hola JAR de Javadoc correspondiente que se ha descargado localmente con el nombre de carpeta de tooa **c:\MyAzureJARs**.

   ![][ic553487]

* *Paso opcional*: haga clic en **Validar**. Posibles problemas con hello JAR de Javadoc podrían mostrarse aquí.

* Haga clic en **Aceptar**.

Una vez asociado con la biblioteca de hello, Hola contenido de Javadoc debe mostrarse en Eclipse IDE. Por ejemplo, si `blob` se define del tipo `CloudBlockBlob` dentro del código, Hola aquí te mostramos un ejemplo de contenido de Javadoc que aparece cuando se escribe `blob.acquireLease` en el código:

![][ic553488]

## <a name="see-also"></a>Otras referencias
[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]

[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
