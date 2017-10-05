---
title: "Solución de problemas de la extensión del panel de acceso de Azure para Internet Explorer | Microsoft Docs"
description: "Cómo usar la directiva de grupo para implementar el complemento de Internet Explorer para el portal de Mis aplicaciones."
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
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="869a1-103">Solución de problemas de la extensión del Panel de acceso para Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="869a1-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="869a1-104">Este artículo le ayudará a solucionar los siguientes problemas:</span><span class="sxs-lookup"><span data-stu-id="869a1-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="869a1-105">No puede tener acceso a sus aplicaciones a través del portal de Mis aplicaciones con Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="869a1-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="869a1-106">Verá el mensaje "Instalar software" aunque ya haya instalado el software.</span><span class="sxs-lookup"><span data-stu-id="869a1-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="869a1-107">Si es administrador, vea también: [Cómo implementar la extensión del Panel de acceso para Internet Explorer con la Directiva de grupo](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="869a1-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="869a1-108">Ejecutar la herramienta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="869a1-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="869a1-109">Puede diagnosticar problemas de instalación con la extensión del Panel de acceso descargando y ejecutando la herramienta de diagnóstico del Panel de acceso:</span><span class="sxs-lookup"><span data-stu-id="869a1-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="869a1-110">Haga clic aquí para descargar la herramienta de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="869a1-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="869a1-111">Abra el archivo y presione el botón **Extraer todo** .</span><span class="sxs-lookup"><span data-stu-id="869a1-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Presionar Extraer todo](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="869a1-113">A continuación, presione el botón **Extraer** para continuar.</span><span class="sxs-lookup"><span data-stu-id="869a1-113">Then press the **Extract** button to continue.</span></span>
   
    ![Presionar Extraer](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="869a1-115">Para ejecutar la herramienta, haga clic con el botón derecho en el archivo denominado **AccessPanelExtensionDiagnosticTool** y, después, seleccione **Abrir con > Host de script basado en Microsoft Windows**.</span><span class="sxs-lookup"><span data-stu-id="869a1-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Abrir con > Host de script basado en Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="869a1-117">A continuación verá la siguiente ventana de diagnóstico, en la que se describe qué puede haber incorrecto con la instalación.</span><span class="sxs-lookup"><span data-stu-id="869a1-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Un ejemplo de la ventana de diagnóstico](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="869a1-119">Haga clic en "**SÍ**" para permitir que el programa corrija los problemas que se han encontrado.</span><span class="sxs-lookup"><span data-stu-id="869a1-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="869a1-120">Para guardar estos cambios, cierre cada ventana de Internet Explorer y luego vuelva a abrir Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="869a1-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="869a1-121">Si todavía no puede tener acceso a sus aplicaciones, pruebe los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="869a1-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="869a1-122">Comprobar que la extensión del Panel de acceso está activada</span><span class="sxs-lookup"><span data-stu-id="869a1-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="869a1-123">Para comprobar que la extensión del Panel de acceso está habilitada en Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="869a1-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="869a1-124">En Internet Explorer, haga clic en el **icono de engranaje** de la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="869a1-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="869a1-125">Después, seleccione **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="869a1-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="869a1-126">(En versiones anteriores de Internet Explorer, encontrará esta opción en **Herramientas > Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="869a1-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Ir a Herramientas > Opciones de Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="869a1-128">Haga clic en la pestaña **Programas** y, después, en el botón **Administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="869a1-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Hacer clic en Administrar complementos](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="869a1-130">En este diálogo, seleccione **Extensión del Panel de acceso** y, después, haga clic en el botón **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="869a1-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Hacer clic en Habilitar](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="869a1-132">Para guardar estos cambios, cierre cada ventana de Internet Explorer y luego vuelva a abrir Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="869a1-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="869a1-133">Habilitar extensiones para la exploración de InPrivate</span><span class="sxs-lookup"><span data-stu-id="869a1-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="869a1-134">Si usa el modo de exploración de InPrivate:</span><span class="sxs-lookup"><span data-stu-id="869a1-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="869a1-135">En Internet Explorer, haga clic en el **icono de engranaje** de la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="869a1-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="869a1-136">Después, seleccione **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="869a1-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="869a1-137">(En versiones anteriores de Internet Explorer, encontrará esta opción en **Herramientas > Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="869a1-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Un ejemplo de la ventana de diagnóstico](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="869a1-139">Vaya a la pestaña **Privacidad** y **desactive** la casilla **Deshabilitar barras de herramientas y extensiones cuando se inicie la exploración de InPrivate**.</span><span class="sxs-lookup"><span data-stu-id="869a1-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Desactivar Deshabilitar barras de herramientas y extensiones cuando se inicie la exploración de InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="869a1-141">Para guardar estos cambios, cierre cada ventana de Internet Explorer y luego vuelva a abrir Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="869a1-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="869a1-142">Desinstalar la extensión del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="869a1-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="869a1-143">Para desinstalar la extensión del Panel de acceso desde el equipo:</span><span class="sxs-lookup"><span data-stu-id="869a1-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="869a1-144">En el teclado, presione la **clave de Windows** para abrir el menú Inicio.</span><span class="sxs-lookup"><span data-stu-id="869a1-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="869a1-145">Cuando se abre el menú, puede escribir cualquier cosa para realizar una búsqueda.</span><span class="sxs-lookup"><span data-stu-id="869a1-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="869a1-146">Escriba "Panel de Control" y luego abra el **Panel de Control** cuando aparezca en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="869a1-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Buscar el Panel de Control](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="869a1-148">En la esquina superior derecha del Panel de control, cambie la opción **Ver** a **Iconos grandes**.</span><span class="sxs-lookup"><span data-stu-id="869a1-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="869a1-149">Luego busque y haga clic en el botón **Programas y características**.</span><span class="sxs-lookup"><span data-stu-id="869a1-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Cambiar la vista para mostrar iconos grandes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="869a1-151">En la lista, seleccione **Access Panel Extension** (Extensión del Panel de acceso) y, después, haga clic en el botón **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="869a1-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Hacer clic en Desinstalar](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="869a1-153">Después, puede intentar instalar la extensión de nuevo para ver si se ha resuelto el problema.</span><span class="sxs-lookup"><span data-stu-id="869a1-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="869a1-154">Si encuentra problemas al desinstalar la extensión, también puede quitarla usando la herramienta [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) .</span><span class="sxs-lookup"><span data-stu-id="869a1-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="869a1-155">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="869a1-155">Related Articles</span></span>
* [<span data-ttu-id="869a1-156">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="869a1-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="869a1-157">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="869a1-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="869a1-158">Implementación de la extensión del Panel de acceso para Internet Explorer mediante la directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="869a1-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

