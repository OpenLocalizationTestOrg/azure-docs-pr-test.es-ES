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
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="76f3b-103">Mostrar el contenido de Javadoc en Eclipse para hello paquete de bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="76f3b-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="76f3b-104">Hola contenido de Javadoc de hello bibliotecas de Azure para Java puede verse en el entorno Eclipse asociando hello toohello contenido de Javadoc bibliotecas de Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="76f3b-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="76f3b-105">Hello pasos siguientes muestran cómo toouse esta funcionalidad en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="76f3b-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="76f3b-106">Este procedimiento se da por supuesto que ya ha agregado hello biblioteca de Azure para la ruta de acceso de compilación de Java tooyour.</span><span class="sxs-lookup"><span data-stu-id="76f3b-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="76f3b-107">toodisplay contenido de Javadoc en Eclipse para hello bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="76f3b-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="76f3b-108">En el Explorador de proyectos de Eclipse, en hello **hace referencia a bibliotecas** menú contextual abierto Hola Hola biblioteca de Azure para JAR de Java, en una sección del proyecto.</span><span class="sxs-lookup"><span data-stu-id="76f3b-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="76f3b-109">Por ejemplo, **microsoft-Windows-api-0.1.0** (número de versión de Hola puede ser diferente, dependiendo de qué versión ha instalado).</span><span class="sxs-lookup"><span data-stu-id="76f3b-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="76f3b-110">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="76f3b-110">Click **Properties**.</span></span>

* <span data-ttu-id="76f3b-111">Dentro de hello **propiedades** cuadro de diálogo, en el panel izquierdo de hello, haga clic en **ubicación de Javadoc**.</span><span class="sxs-lookup"><span data-stu-id="76f3b-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="76f3b-112">Hola **ubicación de Javadoc** se muestra el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="76f3b-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="76f3b-113">Puede especificar una **Javadoc URL** (URL de Javadoc) o un **Javadoc in archive** (Javadoc en archivo).</span><span class="sxs-lookup"><span data-stu-id="76f3b-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="76f3b-114">Si elige toospecify una **dirección URL de Javadoc**, utilice direcciones URL de hello como **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="76f3b-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="76f3b-115">Si elige toouse **Javadoc en archivo**, puede especificar un archivo externo o un archivo de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="76f3b-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="76f3b-116">Realice su elección y examine o valide según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="76f3b-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="76f3b-117">Hello en el ejemplo siguiente se asocia hello Azure Libraries for Java Hola JAR de Javadoc correspondiente que se ha descargado localmente con el nombre de carpeta de tooa **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="76f3b-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="76f3b-118">*Paso opcional*: haga clic en **Validar**.</span><span class="sxs-lookup"><span data-stu-id="76f3b-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="76f3b-119">Posibles problemas con hello JAR de Javadoc podrían mostrarse aquí.</span><span class="sxs-lookup"><span data-stu-id="76f3b-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="76f3b-120">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="76f3b-120">Click **OK**.</span></span>

<span data-ttu-id="76f3b-121">Una vez asociado con la biblioteca de hello, Hola contenido de Javadoc debe mostrarse en Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="76f3b-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="76f3b-122">Por ejemplo, si `blob` se define del tipo `CloudBlockBlob` dentro del código, Hola aquí te mostramos un ejemplo de contenido de Javadoc que aparece cuando se escribe `blob.acquireLease` en el código:</span><span class="sxs-lookup"><span data-stu-id="76f3b-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="76f3b-123">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="76f3b-123">See Also</span></span>
<span data-ttu-id="76f3b-124">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="76f3b-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="76f3b-125">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="76f3b-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="76f3b-126">[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="76f3b-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="76f3b-127">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="76f3b-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
