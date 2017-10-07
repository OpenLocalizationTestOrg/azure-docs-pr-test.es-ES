---
title: "local tooon aaaConnect sistema de archivos de las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conectar sistemas de archivos local tooon del flujo de trabajo de aplicación lógica a través de puerta de enlace de datos de hello en local y el conector de sistema de archivos"
keywords: Sistemas de archivos
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="ab239-104">Conectar sistemas de archivos local tooon desde las aplicaciones lógicas con el conector del sistema de archivos de Hola</span><span class="sxs-lookup"><span data-stu-id="ab239-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="ab239-105">Conectividad de nube híbrida es aplicaciones toologic central, por lo que toomanage datos y segura acceso a recursos locales, las aplicaciones lógicas pueden usar la puerta de enlace de datos de hello en local.</span><span class="sxs-lookup"><span data-stu-id="ab239-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="ab239-106">En este artículo, le mostramos cómo tooconnect tooan local sistema de archivos con un escenario básico: copiar un archivo que tooa tooDropbox cargado recurso compartido de archivos, a continuación, envíe un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="ab239-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab239-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ab239-107">Prerequisites</span></span>

- <span data-ttu-id="ab239-108">Instalar y configurar hello más reciente [puerta de enlace de datos local](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="ab239-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="ab239-109">Instalar hello más reciente local data gateway, versión 1.15.6150.1 o superior.</span><span class="sxs-lookup"><span data-stu-id="ab239-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="ab239-110">[Conectar la puerta de enlace de datos de toohello local](http://aka.ms/logicapps-gateway) listas Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="ab239-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="ab239-111">puerta de enlace de Hello debe instalarse en un equipo local para poder continuar con el resto de Hola de pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab239-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="ab239-112">Agregar desencadenadores y acciones para conectar el sistema de archivos tooyour</span><span class="sxs-lookup"><span data-stu-id="ab239-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="ab239-113">Cree una aplicación de la lógica y agregue el desencadenador **Dropbox - Cuando se crea un archivo**.</span><span class="sxs-lookup"><span data-stu-id="ab239-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="ab239-114">En el desencadenador de hello, elija **paso siguiente** > **agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="ab239-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="ab239-115">En el cuadro de búsqueda de hello, escriba `file system` para que pueda ver todos los admitidos acciones para el conector de sistema de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab239-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Conector Buscar archivo](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="ab239-117">Elija hello **crear archivo** acción y crear un sistema de archivos de conexión tooyour.</span><span class="sxs-lookup"><span data-stu-id="ab239-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="ab239-118">Si no tiene una conexión existente, son toocreate solicitada uno.</span><span class="sxs-lookup"><span data-stu-id="ab239-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="ab239-119">Seleccione **Connect via on-premises data gateway** (Conectarse a través de la puerta de enlace de datos local).</span><span class="sxs-lookup"><span data-stu-id="ab239-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="ab239-120">Aparecen más propiedades.</span><span class="sxs-lookup"><span data-stu-id="ab239-120">More properties appear.</span></span>
   2. <span data-ttu-id="ab239-121">Seleccione la carpeta raíz para el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="ab239-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="ab239-122">Hola raíz carpeta es Hola principales, que se usa para las rutas de acceso relativas para todas las acciones relacionadas con el archivo.</span><span class="sxs-lookup"><span data-stu-id="ab239-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="ab239-123">Puede especificar una carpeta local en el equipo de Hola donde se instala la puerta de enlace de datos de hello en local o carpeta de hello puede ser puede tener acceso un recurso compartido de red que Hola máquina.</span><span class="sxs-lookup"><span data-stu-id="ab239-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="ab239-124">Escriba Hola username y password para puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab239-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="ab239-125">Seleccione la puerta de enlace de Hola que instaló anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab239-125">Select hello gateway that you previously installed.</span></span>

       ![Configuración de la conexión](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="ab239-127">Después de proporcionar todos los detalles de hello, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="ab239-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="ab239-128">Lógica de aplicaciones se configura y comprueba la conexión, asegurándose de que la conexión de hello funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="ab239-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="ab239-129">Si la conexión de hello está configurado correctamente, verá opciones para la acción de Hola que seleccionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab239-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="ab239-130">Conector de sistema de archivos de Hello ahora está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="ab239-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="ab239-131">Especificar que desea toocopy archivos desde la carpeta de Dropbox toohello raíz para el recurso compartido de archivos de local.</span><span class="sxs-lookup"><span data-stu-id="ab239-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Acción Crear archivo](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="ab239-133">Después de su archivo de Hola copias de aplicación lógica, agregar una acción de Outlook que envía un correo electrónico para que usuarios correspondientes saben el nuevo archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab239-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="ab239-134">Especifique los destinatarios de hello, título y cuerpo del mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab239-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="ab239-135">En el selector de contenido dinámico de hello, puede elegir datos salidas de conector de archivos de Hola para que pueda agregar más correo electrónico de toohello de detalles.</span><span class="sxs-lookup"><span data-stu-id="ab239-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Acción Enviar correo electrónico](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="ab239-137">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ab239-137">Save your logic app.</span></span> <span data-ttu-id="ab239-138">Probar la aplicación mediante la carga de un archivo tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="ab239-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="ab239-139">archivo Hello debe obtener el recurso compartido de archivos de toohello copiada en local y debe recibir un correo electrónico acerca de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab239-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="ab239-140">Obtenga información acerca de cómo demasiado[supervisar las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ab239-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="ab239-141">Enhorabuena, ahora tiene una aplicación de lógica de trabajo que se puede conectar el sistema de archivos local tooyour.</span><span class="sxs-lookup"><span data-stu-id="ab239-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="ab239-142">Intente explorar otras funcionalidades que Hola ofertas de conector, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab239-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="ab239-143">Crear archivo</span><span class="sxs-lookup"><span data-stu-id="ab239-143">Create file</span></span>
- <span data-ttu-id="ab239-144">Enumerar archivos de la carpeta</span><span class="sxs-lookup"><span data-stu-id="ab239-144">List files in folder</span></span>
- <span data-ttu-id="ab239-145">Anexar archivo</span><span class="sxs-lookup"><span data-stu-id="ab239-145">Append file</span></span>
- <span data-ttu-id="ab239-146">Eliminar archivo</span><span class="sxs-lookup"><span data-stu-id="ab239-146">Delete file</span></span>
- <span data-ttu-id="ab239-147">Obtener contenido de archivo</span><span class="sxs-lookup"><span data-stu-id="ab239-147">Get file content</span></span>
- <span data-ttu-id="ab239-148">Obtener contenido de archivo mediante la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="ab239-148">Get file content using path</span></span>
- <span data-ttu-id="ab239-149">Obtener metadatos de archivo</span><span class="sxs-lookup"><span data-stu-id="ab239-149">Get file metadata</span></span>
- <span data-ttu-id="ab239-150">Obtener metadatos de archivo mediante la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="ab239-150">Get file metadata using path</span></span>
- <span data-ttu-id="ab239-151">Enumerar archivos de la carpeta raíz</span><span class="sxs-lookup"><span data-stu-id="ab239-151">List files in root folder</span></span>
- <span data-ttu-id="ab239-152">Actualizar archivo</span><span class="sxs-lookup"><span data-stu-id="ab239-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="ab239-153">Swagger de hello de vista</span><span class="sxs-lookup"><span data-stu-id="ab239-153">View hello swagger</span></span>
<span data-ttu-id="ab239-154">Vea hello [swagger detalles](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="ab239-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="ab239-155">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="ab239-155">Get help</span></span>

<span data-ttu-id="ab239-156">tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="ab239-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="ab239-157">toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="ab239-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab239-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab239-158">Next steps</span></span>

- <span data-ttu-id="ab239-159">[Conectar datos locales tooon](../logic-apps/logic-apps-gateway-connection.md) desde las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="ab239-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="ab239-160">Aprenda sobre la [integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab239-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
