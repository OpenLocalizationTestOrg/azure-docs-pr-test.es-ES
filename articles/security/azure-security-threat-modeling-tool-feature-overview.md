---
title: aaaMicrosoft herramienta de modelado de amenazas - Azure | Documentos de Microsoft
description: "Obtenga información acerca de todas las características de hello disponibles en hello herramienta de modelado de amenazas"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="655a8-103">Información general de las características de Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="655a8-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="655a8-104">Nos complace que eligió hello toouse herramienta de modelado de amenazas para sus necesidades de modelado de amenazas.</span><span class="sxs-lookup"><span data-stu-id="655a8-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="655a8-105">Si lo ha hecho, visite  **[Introducción a la herramienta de modelado de amenazas de hello](./azure-security-threat-modeling-tool-getting-started.md)**  conceptos básicos de hello toolearn.</span><span class="sxs-lookup"><span data-stu-id="655a8-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="655a8-106">Nuestra herramienta se actualiza con frecuencia, por lo que compruebe esta guía a menudo toosee nuestras características y mejoras más recientes.</span><span class="sxs-lookup"><span data-stu-id="655a8-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="655a8-107">Al hacer clic en el botón de "Crear un nuevo modelo de" Hola, abre una página de inicio en blanco, una imagen toohello similar a continuación:</span><span class="sxs-lookup"><span data-stu-id="655a8-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Página de inicio en blanco](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="655a8-109">Utilizando el modelo de amenazas de hello creados por nuestro equipo de hello  **[Introducción](./azure-security-threat-modeling-tool-getting-started.md)**  ejemplo, vamos a desproteger todas las características de hello disponibles en la herramienta de hello hoy en día.</span><span class="sxs-lookup"><span data-stu-id="655a8-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Modelo de amenaza básica](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="655a8-111">Navegación</span><span class="sxs-lookup"><span data-stu-id="655a8-111">Navigation</span></span>

<span data-ttu-id="655a8-112">Antes de profundizar en las características integradas de hello, repasemos componentes principales de Hola de herramienta Hola</span><span class="sxs-lookup"><span data-stu-id="655a8-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="655a8-113">Elementos de menú</span><span class="sxs-lookup"><span data-stu-id="655a8-113">Menu items</span></span>

<span data-ttu-id="655a8-114">experiencia de Hello debe ser productos de Microsoft tooother similares.</span><span class="sxs-lookup"><span data-stu-id="655a8-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="655a8-115">Vamos a empezar, vaya a través de los elementos de menú de nivel superior de hello:</span><span class="sxs-lookup"><span data-stu-id="655a8-115">Let’s begin by going through hello top-level menu items:</span></span>

![Elementos de menú](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="655a8-117">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="655a8-117">Label</span></span>                               | <span data-ttu-id="655a8-118">Detalles</span><span class="sxs-lookup"><span data-stu-id="655a8-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="655a8-119">**Archivo**</span><span class="sxs-lookup"><span data-stu-id="655a8-119">**File**</span></span> | <ul><li><span data-ttu-id="655a8-120">Abrir, guardar y cerrar archivos</span><span class="sxs-lookup"><span data-stu-id="655a8-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="655a8-121">Iniciar y cerrar sesión en cuentas de OneDrive</span><span class="sxs-lookup"><span data-stu-id="655a8-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="655a8-122">Compartir vínculos (Vista + Edición)</span><span class="sxs-lookup"><span data-stu-id="655a8-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="655a8-123">Ver información de archivo</span><span class="sxs-lookup"><span data-stu-id="655a8-123">View File Information</span></span></li><li><span data-ttu-id="655a8-124">Aplicar la nueva plantilla tooExisting modelos</span><span class="sxs-lookup"><span data-stu-id="655a8-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="655a8-125">**Edición**</span><span class="sxs-lookup"><span data-stu-id="655a8-125">**Edit**</span></span> | <span data-ttu-id="655a8-126">Acciones de deshacer/rehacer, además de copiar, pegar y eliminar</span><span class="sxs-lookup"><span data-stu-id="655a8-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="655a8-127">**Vista**</span><span class="sxs-lookup"><span data-stu-id="655a8-127">**View**</span></span> | <ul><li><span data-ttu-id="655a8-128">Cambiar entre las vistas **Análisis** y **Diseño**</span><span class="sxs-lookup"><span data-stu-id="655a8-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="655a8-129">Abrir las ventanas cerradas (por ejemplo, galerías de símbolos, propiedades de elementos y mensajes)</span><span class="sxs-lookup"><span data-stu-id="655a8-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="655a8-130">Restablecer la configuración de diseño toodefault.</span><span class="sxs-lookup"><span data-stu-id="655a8-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="655a8-131">**Diagrama**</span><span class="sxs-lookup"><span data-stu-id="655a8-131">**Diagram**</span></span> | <span data-ttu-id="655a8-132">Agregar o eliminar diagramas, y navegar a través de "pestañas" de diagramas</span><span class="sxs-lookup"><span data-stu-id="655a8-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="655a8-133">**Informes**</span><span class="sxs-lookup"><span data-stu-id="655a8-133">**Reports**</span></span> | <span data-ttu-id="655a8-134">Crear tooshare de informes HTML con otras personas</span><span class="sxs-lookup"><span data-stu-id="655a8-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="655a8-135">**Ayuda**</span><span class="sxs-lookup"><span data-stu-id="655a8-135">**Help**</span></span> | <span data-ttu-id="655a8-136">Guía toohelp utilizar herramienta Hola</span><span class="sxs-lookup"><span data-stu-id="655a8-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="655a8-137">iconos de Hello son accesos directos para los menús de nivel superior de hello:</span><span class="sxs-lookup"><span data-stu-id="655a8-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="655a8-138">Icono</span><span class="sxs-lookup"><span data-stu-id="655a8-138">Icon</span></span>                               | <span data-ttu-id="655a8-139">Detalles</span><span class="sxs-lookup"><span data-stu-id="655a8-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="655a8-140">**Abrir**</span><span class="sxs-lookup"><span data-stu-id="655a8-140">**Open**</span></span> | <span data-ttu-id="655a8-141">Abre un nuevo archivo</span><span class="sxs-lookup"><span data-stu-id="655a8-141">Opens a new file</span></span> |
| <span data-ttu-id="655a8-142">**Guardar**</span><span class="sxs-lookup"><span data-stu-id="655a8-142">**Save**</span></span> | <span data-ttu-id="655a8-143">Guarda el archivo actual</span><span class="sxs-lookup"><span data-stu-id="655a8-143">Saves current file</span></span> |
| <span data-ttu-id="655a8-144">**Diseño**</span><span class="sxs-lookup"><span data-stu-id="655a8-144">**Design**</span></span> | <span data-ttu-id="655a8-145">Entra en la vista de diseño, donde puede crear modelos</span><span class="sxs-lookup"><span data-stu-id="655a8-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="655a8-146">**Análisis**</span><span class="sxs-lookup"><span data-stu-id="655a8-146">**Analyze**</span></span> | <span data-ttu-id="655a8-147">Muestra las amenazas generadas y sus propiedades</span><span class="sxs-lookup"><span data-stu-id="655a8-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="655a8-148">**Agregar diagrama**</span><span class="sxs-lookup"><span data-stu-id="655a8-148">**Add Diagram**</span></span> | <span data-ttu-id="655a8-149">Agrega el nuevo diagrama (similar toonew fichas en Excel)</span><span class="sxs-lookup"><span data-stu-id="655a8-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="655a8-150">**Eliminar diagrama**</span><span class="sxs-lookup"><span data-stu-id="655a8-150">**Delete Diagram**</span></span> | <span data-ttu-id="655a8-151">Elimina el diagrama actual</span><span class="sxs-lookup"><span data-stu-id="655a8-151">Deletes current diagram</span></span> |
| <span data-ttu-id="655a8-152">**Copiar/Cortar/Pegar**</span><span class="sxs-lookup"><span data-stu-id="655a8-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="655a8-153">Copia, corta o pega elementos</span><span class="sxs-lookup"><span data-stu-id="655a8-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="655a8-154">**Deshacer/Rehacer**</span><span class="sxs-lookup"><span data-stu-id="655a8-154">**Undo/Redo**</span></span> | <span data-ttu-id="655a8-155">Deshace o rehace acciones</span><span class="sxs-lookup"><span data-stu-id="655a8-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="655a8-156">**Acercar/Alejar**</span><span class="sxs-lookup"><span data-stu-id="655a8-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="655a8-157">Amplía dentro y fuera de diagrama de Hola para obtener una mejor vista</span><span class="sxs-lookup"><span data-stu-id="655a8-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="655a8-158">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="655a8-158">**Feedback**</span></span> | <span data-ttu-id="655a8-159">Se abre Hola foro de MSDN</span><span class="sxs-lookup"><span data-stu-id="655a8-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="655a8-160">Lienzo</span><span class="sxs-lookup"><span data-stu-id="655a8-160">Canvas</span></span>

<span data-ttu-id="655a8-161">espacio de Hola donde arrastrar y colocar elementos en.</span><span class="sxs-lookup"><span data-stu-id="655a8-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="655a8-162">Arrastrar y colocar es más rápida de Hola y modelos de toobuild de manera más eficaces.</span><span class="sxs-lookup"><span data-stu-id="655a8-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="655a8-163">También puede haga clic y seleccione del menú de hello, que agrega las versiones genéricas de los elementos de Hola que está usando, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="655a8-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="655a8-164">Eliminación de galería de símbolos de hello en el lienzo de Hola</span><span class="sxs-lookup"><span data-stu-id="655a8-164">Dropping hello stencil on hello canvas</span></span>

![Colocación en el lienzo](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="655a8-166">Al hacer clic en la Galería de símbolos de Hola</span><span class="sxs-lookup"><span data-stu-id="655a8-166">Clicking on hello stencil</span></span>

![Propiedades del elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="655a8-168">Galerías de símbolos</span><span class="sxs-lookup"><span data-stu-id="655a8-168">Stencils</span></span>

<span data-ttu-id="655a8-169">Donde puede encontrar todas las galerías de símbolos disponible toouse basado en plantilla Hola seleccionada.</span><span class="sxs-lookup"><span data-stu-id="655a8-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="655a8-170">Si no encuentra los elementos adecuados de hello, intente usar otra plantilla o modificar una toofit sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="655a8-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="655a8-171">Por lo general, debe ser capaz de toofind una combinación de categorías como Hola que a continuación:</span><span class="sxs-lookup"><span data-stu-id="655a8-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="655a8-172">Nombre de la galería de símbolos</span><span class="sxs-lookup"><span data-stu-id="655a8-172">Stencil Name</span></span>                               | <span data-ttu-id="655a8-173">Detalles</span><span class="sxs-lookup"><span data-stu-id="655a8-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="655a8-174">**Proceso**</span><span class="sxs-lookup"><span data-stu-id="655a8-174">**Process**</span></span> | <span data-ttu-id="655a8-175">Aplicaciones, complementos de explorador, subprocesos, máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="655a8-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="655a8-176">**External Interactor** (Interactivo externo)</span><span class="sxs-lookup"><span data-stu-id="655a8-176">**External Interactor**</span></span> | <span data-ttu-id="655a8-177">Proveedores de autenticación, exploradores, usuarios, aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="655a8-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="655a8-178">**Almacén de datos**</span><span class="sxs-lookup"><span data-stu-id="655a8-178">**Data Store**</span></span> | <span data-ttu-id="655a8-179">Caché, almacenamiento, archivos de configuración, bases de datos, Registro</span><span class="sxs-lookup"><span data-stu-id="655a8-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="655a8-180">**Flujo de datos**</span><span class="sxs-lookup"><span data-stu-id="655a8-180">**Data Flow**</span></span> | <span data-ttu-id="655a8-181">Binario, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Canalización con nombre, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="655a8-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="655a8-182">**Trust Line/Border Boundary** (Línea de confianza/Línea de borde)</span><span class="sxs-lookup"><span data-stu-id="655a8-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="655a8-183">Redes corporativas, Internet, máquina, espacio aislado, modo Kernel/Usuario</span><span class="sxs-lookup"><span data-stu-id="655a8-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="655a8-184">Notas/Mensajes</span><span class="sxs-lookup"><span data-stu-id="655a8-184">Notes/Messages</span></span>

| <span data-ttu-id="655a8-185">Componente</span><span class="sxs-lookup"><span data-stu-id="655a8-185">Component</span></span>                               | <span data-ttu-id="655a8-186">Detalles</span><span class="sxs-lookup"><span data-stu-id="655a8-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="655a8-187">**Mensajes**</span><span class="sxs-lookup"><span data-stu-id="655a8-187">**Messages**</span></span> | <span data-ttu-id="655a8-188">Lógica de herramienta interna que alerta a los usuarios cada vez que hay un error, por ejemplo, cuando no hay flujos de datos entre los elementos</span><span class="sxs-lookup"><span data-stu-id="655a8-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="655a8-189">**Notas**</span><span class="sxs-lookup"><span data-stu-id="655a8-189">**Notes**</span></span> | <span data-ttu-id="655a8-190">Notas manuales archivo toohello agregado por los equipos de ingeniería en su totalidad Hola diseño y proceso de revisión</span><span class="sxs-lookup"><span data-stu-id="655a8-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="655a8-191">Propiedades del elemento</span><span class="sxs-lookup"><span data-stu-id="655a8-191">Element properties</span></span>

<span data-ttu-id="655a8-192">Éstos varían según los elementos de hello seleccionados.</span><span class="sxs-lookup"><span data-stu-id="655a8-192">These vary by hello elements selected.</span></span> <span data-ttu-id="655a8-193">Además de los límites de confianza, todos los demás elementos contienen tres selecciones generales:</span><span class="sxs-lookup"><span data-stu-id="655a8-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="655a8-194">Propiedad de elemento</span><span class="sxs-lookup"><span data-stu-id="655a8-194">Element Property</span></span>                               | <span data-ttu-id="655a8-195">Detalles</span><span class="sxs-lookup"><span data-stu-id="655a8-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="655a8-196">**Name**</span><span class="sxs-lookup"><span data-stu-id="655a8-196">**Name**</span></span> | <span data-ttu-id="655a8-197">Útil para asignar nombres a su toobe de procesos, almacenes, interactuadores y flujos reconocido con facilidad</span><span class="sxs-lookup"><span data-stu-id="655a8-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="655a8-198">**Out of Scope** (Fuera de ámbito)</span><span class="sxs-lookup"><span data-stu-id="655a8-198">**Out of Scope**</span></span> | <span data-ttu-id="655a8-199">Si se selecciona, el elemento de Hola se saca de matriz de generación de amenaza de hello (no recomendado)</span><span class="sxs-lookup"><span data-stu-id="655a8-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="655a8-200">**Reason for Out of Scope** (Motivo de elegir Fuera de ámbito)</span><span class="sxs-lookup"><span data-stu-id="655a8-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="655a8-201">Los usuarios de toolet de campo de justificación saben por qué se seleccionó fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="655a8-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="655a8-202">Se cambian las propiedades de cada categoría de elemento.</span><span class="sxs-lookup"><span data-stu-id="655a8-202">Properties are changed under each element category.</span></span> <span data-ttu-id="655a8-203">Haga clic en cada opciones disponibles de elemento tooinspect hello, o abra Hola plantilla toolearn más.</span><span class="sxs-lookup"><span data-stu-id="655a8-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="655a8-204">Comencemos con características de Hola.</span><span class="sxs-lookup"><span data-stu-id="655a8-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="655a8-205">Pantalla principal</span><span class="sxs-lookup"><span data-stu-id="655a8-205">Welcome screen</span></span>

<span data-ttu-id="655a8-206">pantalla de bienvenida de Hello es Hola primera cosa que verá cuando se abre la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="655a8-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="655a8-207">Abrir un modelo</span><span class="sxs-lookup"><span data-stu-id="655a8-207">Open A model</span></span>

<span data-ttu-id="655a8-208">Al mantener el mouse sobre el botón "Abrir un modelo", se muestran dos opciones ocultas: "Abrir desde este equipo" y "Abrir desde OneDrive".</span><span class="sxs-lookup"><span data-stu-id="655a8-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="655a8-209">Hola abre por primera vez abrir archivo pantalla de bienvenida, mientras hello en segundo lugar le guiará por inicio de sesión de hello en proceso para OneDrive, permitiéndole toopick carpetas y archivos después de una autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="655a8-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Abrir modelo](./media/azure-security-threat-modeling-tool/openmodel.png)

![Abrir desde el equipo o desde OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="655a8-212">Comentarios, sugerencias y problemas</span><span class="sxs-lookup"><span data-stu-id="655a8-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="655a8-213">Al seleccionar esta opción le permitirán toohello foros de MSDN para herramientas de SDL.</span><span class="sxs-lookup"><span data-stu-id="655a8-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="655a8-214">Es un toocheck excelente manera a otras personas opinión acerca de la herramienta de hello, incluidas nuevas ideas y soluciones.</span><span class="sxs-lookup"><span data-stu-id="655a8-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Comentarios](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="655a8-216">Vista de diseño</span><span class="sxs-lookup"><span data-stu-id="655a8-216">Design view</span></span>

<span data-ttu-id="655a8-217">Cada vez que abra o cree un nuevo modelo, se le dirigirá toohello la vista de diseño.</span><span class="sxs-lookup"><span data-stu-id="655a8-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="655a8-218">Adición de elementos</span><span class="sxs-lookup"><span data-stu-id="655a8-218">Adding elements</span></span>

<span data-ttu-id="655a8-219">Hay 2 formas tooadd elementos en la cuadrícula de hello:</span><span class="sxs-lookup"><span data-stu-id="655a8-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="655a8-220">**Arrastrar y colocar** : arrastre Hola elemento deseado toohello cuadrícula, utilice la información adicional de hello elemento Propiedades tooprovide.</span><span class="sxs-lookup"><span data-stu-id="655a8-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="655a8-221">**Haga clic en** : haga clic en cualquier parte en la cuadrícula de Hola y seleccione del menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="655a8-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="655a8-222">Una representación genérica de ese elemento aparecerá en la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="655a8-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="655a8-223">Conexión de elementos</span><span class="sxs-lookup"><span data-stu-id="655a8-223">Connecting elements</span></span>

<span data-ttu-id="655a8-224">Hay 2 formas tooconnect elementos en la herramienta de hello:</span><span class="sxs-lookup"><span data-stu-id="655a8-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="655a8-225">**Arrastrar y colocar** : arrastre cuadrícula de toohello de flujo de datos deseada de Hola y conectar ambos elementos correspondientes de toohello de extremos.</span><span class="sxs-lookup"><span data-stu-id="655a8-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="655a8-226">**Haga clic en + MAYÚS** : haga clic en el primer elemento de hello (enviar datos), presione y mantenga presionada MAYÚS hello y, a continuación, segundo elemento de hello seleccione (recibir datos).</span><span class="sxs-lookup"><span data-stu-id="655a8-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="655a8-227">Haga clic con el botón derecho y seleccione "Conectar".</span><span class="sxs-lookup"><span data-stu-id="655a8-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="655a8-228">Si usa un flujo de datos bidireccional, orden de hello no es tan importante.</span><span class="sxs-lookup"><span data-stu-id="655a8-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="655a8-229">Propiedades</span><span class="sxs-lookup"><span data-stu-id="655a8-229">Properties</span></span>

<span data-ttu-id="655a8-230">Muestra todas las propiedades de Hola que pueden modificarse en galerías de símbolos de hello colocados en el diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="655a8-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="655a8-231">propiedades de hello toosee, haga clic en la Galería de símbolos de Hola y Hola se rellena en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="655a8-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="655a8-232">ejemplo de Hola siguiente se muestra antes y después de una galería de símbolos se arrastra hasta el diagrama de Hola de "base de datos":</span><span class="sxs-lookup"><span data-stu-id="655a8-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="655a8-233">Antes</span><span class="sxs-lookup"><span data-stu-id="655a8-233">Before</span></span>

![Antes](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="655a8-235">Después</span><span class="sxs-lookup"><span data-stu-id="655a8-235">After</span></span>

![Después](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="655a8-237">error de Hadoop</span><span class="sxs-lookup"><span data-stu-id="655a8-237">Messages</span></span>

<span data-ttu-id="655a8-238">Si crea un modelo de amenazas y olvidarse de fluyen de datos de tooconnect tooelements, ventana de mensaje de Hola notifica tooact.</span><span class="sxs-lookup"><span data-stu-id="655a8-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="655a8-239">Puede elegir tooignore lo o seguimiento Hola problema de instrucciones toofix Hola.</span><span class="sxs-lookup"><span data-stu-id="655a8-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![error de Hadoop](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="655a8-241">Notas</span><span class="sxs-lookup"><span data-stu-id="655a8-241">Notes</span></span>

<span data-ttu-id="655a8-242">Cambiar de fichas de tooNotes de mensajes permite tooadd notas tooyour diagrama toocapture todas sus ideas</span><span class="sxs-lookup"><span data-stu-id="655a8-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="655a8-243">Vista de análisis</span><span class="sxs-lookup"><span data-stu-id="655a8-243">Analysis view</span></span>

<span data-ttu-id="655a8-244">Cuando haya finalizado de crear el diagrama, cambiar vista tooanalysis al toohello selecciones de menú superior y elegir la paleta de pintura de hello lupa siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="655a8-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Vista de análisis](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="655a8-246">Selección de amenaza generada</span><span class="sxs-lookup"><span data-stu-id="655a8-246">Generated threat selection</span></span>

<span data-ttu-id="655a8-247">Al hacer clic en una amenaza, puede sacar provecho de tres funciones únicas:</span><span class="sxs-lookup"><span data-stu-id="655a8-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="655a8-248">Característica</span><span class="sxs-lookup"><span data-stu-id="655a8-248">Feature</span></span>                               | <span data-ttu-id="655a8-249">Información</span><span class="sxs-lookup"><span data-stu-id="655a8-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="655a8-250">**Indicador de leído**</span><span class="sxs-lookup"><span data-stu-id="655a8-250">**Read Indicator**</span></span> | <p><span data-ttu-id="655a8-251">Amenaza ahora está marcada como lectura, que puede ayudarle fácilmente a realizar un seguimiento de elementos de hello que ha completado ya</span><span class="sxs-lookup"><span data-stu-id="655a8-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Indicador de leído o no leído](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="655a8-253">**Foco de interacción**</span><span class="sxs-lookup"><span data-stu-id="655a8-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="655a8-254">Se resalta la interacción en el diagrama de Hola que pertenece la amenaza de toothat</span><span class="sxs-lookup"><span data-stu-id="655a8-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Foco de interacción](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="655a8-256">**Thread Properties** (Propiedades de amenaza)</span><span class="sxs-lookup"><span data-stu-id="655a8-256">**Threat Properties**</span></span> | <p><span data-ttu-id="655a8-257">Información adicional acerca de la amenaza de Hola se rellena en la ventana de propiedades de amenaza de Hola</span><span class="sxs-lookup"><span data-stu-id="655a8-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Thread Properties (Propiedades de amenaza)](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="655a8-259">Priority change (Cambio de prioridad)</span><span class="sxs-lookup"><span data-stu-id="655a8-259">Priority change</span></span>

<span data-ttu-id="655a8-260">Nivel de prioridad de Hola de cada amenaza generado también se cambia su toomake de colores se tooidentify fácil amenazas de prioridad alta, Media y baja.</span><span class="sxs-lookup"><span data-stu-id="655a8-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Priority change (Cambio de prioridad)](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="655a8-262">Campos modificables de las propiedades de amenaza</span><span class="sxs-lookup"><span data-stu-id="655a8-262">Threat properties editable fields</span></span>

<span data-ttu-id="655a8-263">Tal como se muestra en la imagen de hello anterior, los usuarios pueden cambiar información Hola Hola herramienta generada un también agregar campos de toocertain de información, como la justificación.</span><span class="sxs-lookup"><span data-stu-id="655a8-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="655a8-264">Estos campos son generados por la plantilla de hello, por lo que si necesita más información para cada amenaza, le recomienda toomake modificaciones.</span><span class="sxs-lookup"><span data-stu-id="655a8-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Thread Properties (Propiedades de amenaza)](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="655a8-266">Informes</span><span class="sxs-lookup"><span data-stu-id="655a8-266">Reports</span></span>

<span data-ttu-id="655a8-267">Una vez que haya terminado las prioridades cambiantes y actualización de Hola de estado de cada uno generado amenaza, puede guardar el archivo hello o imprimir un informe desde demasiado "informes" y, a continuación, "Crear informe completo."</span><span class="sxs-lookup"><span data-stu-id="655a8-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="655a8-268">Se le preguntará tooname informe de Hola y cuando lo haga, debería ver algo similar imagen toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="655a8-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Informe](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="655a8-270">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="655a8-270">Next steps</span></span>

<span data-ttu-id="655a8-271">toocontribute una plantilla para la Comunidad de hello, vaya tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  página.</span><span class="sxs-lookup"><span data-stu-id="655a8-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="655a8-272">**[Descargar](https://aka.ms/tmtpreview)**  Hola herramienta tooget comenzar hoy.</span><span class="sxs-lookup"><span data-stu-id="655a8-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
