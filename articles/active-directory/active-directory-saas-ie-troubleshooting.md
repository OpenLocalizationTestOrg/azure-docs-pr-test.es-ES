---
title: "Hola aaaTroubleshooting extensión del Panel de acceso de Azure para Internet Explorer | Documentos de Microsoft"
description: "¿Cómo toouse grupo complemento de Internet Explorer de directiva toodeploy Hola para portal mis aplicaciones de Hola."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="29046-103">Solución de problemas de hello extensión del Panel de acceso de Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="29046-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="29046-104">En este artículo le ayudará a solucionar Hola los siguientes problemas:</span><span class="sxs-lookup"><span data-stu-id="29046-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="29046-105">Se está tooaccess no se pueden las aplicaciones a través del portal mis aplicaciones de Hola durante el uso de Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="29046-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="29046-106">Vea "Instalar Software" mensaje incluso si ya ha instalado software de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="29046-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="29046-107">Si es administrador, vea también: [cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="29046-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="29046-108">Ejecutar la herramienta de diagnóstico de Hola</span><span class="sxs-lookup"><span data-stu-id="29046-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="29046-109">Puede diagnosticar problemas de instalación con hello extensión del Panel de acceso mediante la descarga y ejecuta la herramienta de diagnóstico de hello Panel de acceso:</span><span class="sxs-lookup"><span data-stu-id="29046-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="29046-110">Haga clic aquí herramienta de diagnóstico de toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="29046-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="29046-111">Archivo abierto hello y presione **extraer todo** botón.</span><span class="sxs-lookup"><span data-stu-id="29046-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Presionar Extraer todo](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="29046-113">A continuación, presione hello **extraer** toocontinue de botón.</span><span class="sxs-lookup"><span data-stu-id="29046-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Presionar Extraer](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="29046-115">herramienta de hello toorun, archivo de hello contextual denominado **AccessPanelExtensionDiagnosticTool**, a continuación, seleccione **abrir con > Microsoft Windows Script Host de**.</span><span class="sxs-lookup"><span data-stu-id="29046-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Abrir con > Host de script basado en Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="29046-117">A continuación, verá Hola después de la ventana de diagnóstico, que describe qué puede ser incorrecto con la instalación.</span><span class="sxs-lookup"><span data-stu-id="29046-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Un ejemplo de ventana de diagnóstico de hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="29046-119">Haga clic en "**Sí**" toolet Hola corrección Hola problemas de programas que se han encontrado.</span><span class="sxs-lookup"><span data-stu-id="29046-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="29046-120">toosave estos cambios, cierre cada ventana de Internet Explorer y, a continuación, vuelva a abrir Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="29046-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="29046-121">Si todavía no se puede obtener acceso a las aplicaciones, intente Hola pasos a continuación.</span><span class="sxs-lookup"><span data-stu-id="29046-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="29046-122">Compruebe que Hola que está habilitada la extensión del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="29046-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="29046-123">tooverify que Hola extensión del Panel de acceso está habilitada en Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="29046-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="29046-124">En Internet Explorer, haga clic en hello **icono de engranaje** en hello superior derecho de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="29046-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="29046-125">Después, seleccione **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="29046-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="29046-126">(En versiones anteriores de Internet Explorer, encontrará esta opción en **Herramientas > Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="29046-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Vaya tooTools > Opciones de Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="29046-128">Haga clic en hello **programas** ficha, a continuación, haga clic en hello **administrar complementos** botón.</span><span class="sxs-lookup"><span data-stu-id="29046-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Hacer clic en Administrar complementos](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="29046-130">En este cuadro de diálogo, seleccione **extensión del Panel de acceso** y, a continuación, haga clic en hello **habilitar** botón.</span><span class="sxs-lookup"><span data-stu-id="29046-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Hacer clic en Habilitar](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="29046-132">toosave estos cambios, se cierra cada ventana de Internet Explorer y, a continuación, vuelva a abrir Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="29046-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="29046-133">Habilitar extensiones para la exploración de InPrivate</span><span class="sxs-lookup"><span data-stu-id="29046-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="29046-134">Si se usa el modo de exploración de InPrivate hello:</span><span class="sxs-lookup"><span data-stu-id="29046-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="29046-135">En Internet Explorer, haga clic en hello **icono de engranaje** en hello superior derecho de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="29046-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="29046-136">Después, seleccione **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="29046-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="29046-137">(En versiones anteriores de Internet Explorer, encontrará esta opción en **Herramientas > Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="29046-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Un ejemplo de ventana de diagnóstico de hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="29046-139">Vaya toohello **privacidad** ficha, a continuación, **desactive** Hola casilla **deshabilitar las barras de herramientas y extensiones cuando se inicia la exploración de InPrivate**</span><span class="sxs-lookup"><span data-stu-id="29046-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Desactivar Deshabilitar barras de herramientas y extensiones cuando se inicie la exploración de InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="29046-141">toosave estos cambios, se cierra cada ventana de Internet Explorer y, a continuación, vuelva a abrir Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="29046-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="29046-142">Desinstalar Hola extensión del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="29046-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="29046-143">Hola toouninstall extensión del Panel de acceso del equipo:</span><span class="sxs-lookup"><span data-stu-id="29046-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="29046-144">En el teclado, presione hello **tecla Windows** menú de inicio de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="29046-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="29046-145">Cuando se abre el menú de hello, puede escribir cualquier cosa toodo una búsqueda.</span><span class="sxs-lookup"><span data-stu-id="29046-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="29046-146">Escriba "Panel de Control" y, a continuación, abra hello **el Panel de Control** cuando aparece en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="29046-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Buscar el Panel de Control](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="29046-148">En hello esquina superior derecha del Panel de Control de Hola, cambie hello **ver** opción demasiado**iconos grandes**.</span><span class="sxs-lookup"><span data-stu-id="29046-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="29046-149">A continuación, busque y haga clic en hello **programas y características** botón.</span><span class="sxs-lookup"><span data-stu-id="29046-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Cambios Hola vista tooshow iconos grandes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="29046-151">En la lista de hello, seleccione **extensión del Panel de acceso**y haga clic en Hola de hello **desinstalar** botón.</span><span class="sxs-lookup"><span data-stu-id="29046-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Hacer clic en Desinstalar](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="29046-153">A continuación, puede intentar extensión de hello tooinstall nuevo toosee si se ha solucionado el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="29046-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="29046-154">Si encuentra problemas al desinstalar la extensión de hello, también puede quitar mediante hello [Microsoft repararlo](https://go.microsoft.com/?linkid=9779673) herramienta.</span><span class="sxs-lookup"><span data-stu-id="29046-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="29046-155">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="29046-155">Related Articles</span></span>
* [<span data-ttu-id="29046-156">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29046-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="29046-157">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29046-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="29046-158">¿Cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="29046-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

