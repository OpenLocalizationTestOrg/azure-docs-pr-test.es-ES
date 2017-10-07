---
title: aaaConfigure CHAP para el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo tooconfigure Hola protocolo de autenticación por desafío mutuo (CHAP) en un dispositivo de StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="685ce-103">Configurar CHAP para el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="685ce-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="685ce-104">Este tutorial le explica cómo tooconfigure CHAP para el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="685ce-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="685ce-105">procedimiento de Hello detallado en este artículo aplica a dispositivos serie 8000 de tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="685ce-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="685ce-106">CHAP significa Protocolo de autenticación por desafío mutuo.</span><span class="sxs-lookup"><span data-stu-id="685ce-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="685ce-107">Es un esquema de autenticación usado por identidad de hello toovalidate de servidores de clientes remotos.</span><span class="sxs-lookup"><span data-stu-id="685ce-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="685ce-108">comprobación de Hola se basa en una contraseña compartida o un secreto.</span><span class="sxs-lookup"><span data-stu-id="685ce-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="685ce-109">CHAP puede ser unidireccional o mutuo (bidireccional).</span><span class="sxs-lookup"><span data-stu-id="685ce-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="685ce-110">Una manera de CHAP es cuando el destino de hello autentica como iniciador.</span><span class="sxs-lookup"><span data-stu-id="685ce-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="685ce-111">En CHAP bidireccional o mutuo, destino de hello autentica el iniciador de hello y, a continuación, iniciador Hola autentica destino Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="685ce-112">La autenticación del iniciador puede implementarse sin la autenticación del destino.</span><span class="sxs-lookup"><span data-stu-id="685ce-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="685ce-113">Sin embargo, la autenticación del destino solo puede implementarse si también se implementa la autenticación del iniciador.</span><span class="sxs-lookup"><span data-stu-id="685ce-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="685ce-114">Como práctica recomendada, se recomienda que utilice la seguridad CHAP tooenhance iSCSI.</span><span class="sxs-lookup"><span data-stu-id="685ce-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="685ce-115">Tenga en cuenta que los dispositivos StorSimple no admiten IPSEC actualmente.</span><span class="sxs-lookup"><span data-stu-id="685ce-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="685ce-116">configuración de CHAP Hello en dispositivo de StorSimple de hello puede configurarse en hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="685ce-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="685ce-117">Autenticación unidireccional</span><span class="sxs-lookup"><span data-stu-id="685ce-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="685ce-118">Autenticación bidireccional o mutua o inversa</span><span class="sxs-lookup"><span data-stu-id="685ce-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="685ce-119">En cada uno de estos casos, el portal de Hola para dispositivo de Hola y el software del iniciador de iSCSI de hello server necesita toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="685ce-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="685ce-120">Hello pasos detallados para esta configuración se describen en hello siguiendo el tutorial.</span><span class="sxs-lookup"><span data-stu-id="685ce-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="685ce-121">Autenticación unidireccional</span><span class="sxs-lookup"><span data-stu-id="685ce-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="685ce-122">En la autenticación unidireccional, destino Hola autentica el iniciador de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="685ce-123">Esta autenticación requiere que configure valores del iniciador de CHAP hello en dispositivo de StorSimple de Hola y Hola iSCSI software Initiator en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="685ce-124">Hola procedimientos detallados para el dispositivo StorSimple y host de Windows se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="685ce-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="685ce-125">tooconfigure el dispositivo para la autenticación unidireccional</span><span class="sxs-lookup"><span data-stu-id="685ce-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="685ce-126">Hola portal de Azure, vaya tooyour servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="685ce-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="685ce-127">Haga clic en **dispositivos** y seleccione y haga clic en un dispositivo que se va tooconfigure CHAP para.</span><span class="sxs-lookup"><span data-stu-id="685ce-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="685ce-128">Vaya demasiado**configuración del dispositivo > seguridad**.</span><span class="sxs-lookup"><span data-stu-id="685ce-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="685ce-129">Hola **configuración de seguridad** hoja, haga clic en **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="685ce-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Iniciador de CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="685ce-131">Hola **CHAP** hoja y en hello **iniciador CHAP** sección:</span><span class="sxs-lookup"><span data-stu-id="685ce-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="685ce-132">Proporcione un nombre de usuario para su iniciador de CHAP.</span><span class="sxs-lookup"><span data-stu-id="685ce-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="685ce-133">Proporcionar una contraseña para su iniciador de CHAP.</span><span class="sxs-lookup"><span data-stu-id="685ce-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="685ce-134">nombre de usuario CHAP Hola debe contener menos de 233 caracteres.</span><span class="sxs-lookup"><span data-stu-id="685ce-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="685ce-135">Contraseña CHAP de Hello debe tener entre 12 y 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="685ce-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="685ce-136">Un nombre de usuario o una contraseña más larga da como resultado un error de autenticación en el host de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="685ce-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="685ce-137">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-137">Confirm hello password.</span></span>

       ![Iniciador de CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="685ce-139">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="685ce-139">Click **Save**.</span></span> <span data-ttu-id="685ce-140">Se muestra un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="685ce-140">A confirmation message is displayed.</span></span> <span data-ttu-id="685ce-141">Haga clic en **Aceptar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="685ce-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="685ce-142">servidor de host tooconfigure autenticación unidireccional en Windows hello</span><span class="sxs-lookup"><span data-stu-id="685ce-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="685ce-143">En el servidor de host de Windows hello, inicie el iniciador iSCSI de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="685ce-144">Hola **propiedades del iniciador iSCSI** ventana, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="685ce-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="685ce-145">Haga clic en hello **detección** ficha.</span><span class="sxs-lookup"><span data-stu-id="685ce-145">Click hello **Discovery** tab.</span></span>
      
       ![Propiedades del iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="685ce-147">Haga clic en **Detectar portal**.</span><span class="sxs-lookup"><span data-stu-id="685ce-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="685ce-148">Hola **detectar Portal de destino** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="685ce-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="685ce-149">Especifique la dirección IP de hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="685ce-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="685ce-150">Haga clic en **Avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="685ce-150">Click **Advanced**.</span></span>
      
       ![Detectar portal de destino](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="685ce-152">Hola **configuración avanzada** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="685ce-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="685ce-153">Seleccione hello **inicio de sesión habilitar CHAP** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="685ce-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="685ce-154">Hola **nombre** campo, nombre de usuario de Hola de fuente de alimentación que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="685ce-155">Hola **secreto de destino** campo, una fuente de alimentación Hola contraseña que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="685ce-156">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="685ce-156">Click **OK**.</span></span>
      
       ![General - Configuración avanzada](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="685ce-158">En hello **destinos** ficha de hello **propiedades del iniciador iSCSI** ventana, el estado del dispositivo Hola debe aparecer como **conectado**.</span><span class="sxs-lookup"><span data-stu-id="685ce-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="685ce-159">Si usa un dispositivo StorSimple 1200, cada volumen se monta como un destino iSCSI.</span><span class="sxs-lookup"><span data-stu-id="685ce-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="685ce-160">Por lo tanto, los pasos 3 y 4 será necesario toobe repite para cada volumen.</span><span class="sxs-lookup"><span data-stu-id="685ce-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volúmenes montados como destinos independientes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="685ce-162">Si cambia el nombre de iSCSI de hello, Hola nuevo nombre se usa para nuevas sesiones de iSCSI.</span><span class="sxs-lookup"><span data-stu-id="685ce-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="685ce-163">La nueva configuración no se utiliza para las sesiones existentes hasta que cierra sesión y vuelve a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="685ce-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="685ce-164">Para obtener más información sobre cómo configurar CHAP en el servidor de host de Windows hello, vaya demasiado[consideraciones adicionales](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="685ce-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="685ce-165">Autenticación bidireccional o mutua</span><span class="sxs-lookup"><span data-stu-id="685ce-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="685ce-166">En la autenticación bidireccional, destino de hello autentica el iniciador de hello y, a continuación, iniciador Hola autentica destino Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="685ce-167">Este procedimiento requiere valores del iniciador CHAP de hello usuario tooconfigure hello, invertir la configuración de CHAP en dispositivo de Hola y software en el host de hello del iniciador iSCSI.</span><span class="sxs-lookup"><span data-stu-id="685ce-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="685ce-168">Hello procedimientos siguientes describen la autenticación mutua de hello pasos tooconfigure en el dispositivo de Hola y en el host de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="685ce-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="685ce-169">tooconfigure el dispositivo para la autenticación mutua</span><span class="sxs-lookup"><span data-stu-id="685ce-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="685ce-170">Hola portal de Azure, vaya tooyour servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="685ce-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="685ce-171">Haga clic en **dispositivos** y seleccione y haga clic en un dispositivo que se va tooconfigure CHAP para.</span><span class="sxs-lookup"><span data-stu-id="685ce-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="685ce-172">Vaya demasiado**configuración del dispositivo > seguridad**.</span><span class="sxs-lookup"><span data-stu-id="685ce-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="685ce-173">Hola **configuración de seguridad** hoja, haga clic en **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="685ce-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Destino de CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="685ce-175">Desplácese hacia abajo en esta página y en hello **destino CHAP** sección:</span><span class="sxs-lookup"><span data-stu-id="685ce-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="685ce-176">Proporcione un **Nombre de usuario de CHAP inverso** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="685ce-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="685ce-177">Proporcione una **Contraseña de CHAP inverso** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="685ce-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="685ce-178">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-178">Confirm hello password.</span></span>
3. <span data-ttu-id="685ce-179">Hola **iniciador CHAP** sección:</span><span class="sxs-lookup"><span data-stu-id="685ce-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="685ce-180">Proporcione un **nombre de usuario** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="685ce-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="685ce-181">Proporcione una **contraseña** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="685ce-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="685ce-182">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-182">Confirm hello password.</span></span>

       ![Iniciador de CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="685ce-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="685ce-184">Click **Save**.</span></span> <span data-ttu-id="685ce-185">Se muestra un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="685ce-185">A confirmation message is displayed.</span></span> <span data-ttu-id="685ce-186">Haga clic en **Aceptar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="685ce-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="685ce-187">servidor de host de la autenticación bidireccional tooconfigure en Windows hello</span><span class="sxs-lookup"><span data-stu-id="685ce-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="685ce-188">En el servidor de host de Windows hello, inicie el iniciador iSCSI de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="685ce-189">Hola **propiedades del iniciador iSCSI** ventana, haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="685ce-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="685ce-190">Haga clic en **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="685ce-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="685ce-191">Hola **secreto CHAP mutuo del iniciador iSCSI** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="685ce-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="685ce-192">Hola de tipo **contraseña de CHAP inverso** que configuró en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="685ce-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="685ce-193">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="685ce-193">Click **OK**.</span></span>
      
       ![Secreto CHAP mutuo del iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="685ce-195">Haga clic en hello **destinos** ficha.</span><span class="sxs-lookup"><span data-stu-id="685ce-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="685ce-196">Haga clic en hello **conectar** botón.</span><span class="sxs-lookup"><span data-stu-id="685ce-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="685ce-197">Hola **conectar tooTarget** cuadro de diálogo, haga clic en **avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="685ce-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="685ce-198">Hola **propiedades avanzadas** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="685ce-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="685ce-199">Seleccione hello **inicio de sesión habilitar CHAP** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="685ce-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="685ce-200">Hola **nombre** campo, nombre de usuario de Hola de fuente de alimentación que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="685ce-201">Hola **secreto de destino** campo, una fuente de alimentación Hola contraseña que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="685ce-202">Seleccione hello **realizar autenticación mutua** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="685ce-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Autenticación mutua de configuración avanzada](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="685ce-204">Haga clic en **Aceptar** configuración de CHAP hello toocomplete</span><span class="sxs-lookup"><span data-stu-id="685ce-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="685ce-205">Para obtener más información sobre cómo configurar CHAP en el servidor de host de Windows hello, vaya demasiado[consideraciones adicionales](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="685ce-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="685ce-206">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="685ce-206">Additional considerations</span></span>

<span data-ttu-id="685ce-207">Hola **conexión rápida** característica no admite conexiones con CHAP habilitado.</span><span class="sxs-lookup"><span data-stu-id="685ce-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="685ce-208">Cuando CHAP esté habilitado, asegúrese de que utiliza hello **conectar** botón que está disponible en hello **destinos** destino de tooa tooconnect de pestaña.</span><span class="sxs-lookup"><span data-stu-id="685ce-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Conectar tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="685ce-210">Hola **conectar tooTarget** cuadro de diálogo es hello presentan, seleccione **agregar esta lista de toohello de conexión de destinos favoritos** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="685ce-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="685ce-211">Esta selección garantiza que cada vez que se reinicie el equipo de hello, se realiza un intento toorestore Hola conexión toohello favoritos los destinos iSCSI.</span><span class="sxs-lookup"><span data-stu-id="685ce-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="685ce-212">Errores durante la configuración</span><span class="sxs-lookup"><span data-stu-id="685ce-212">Errors during configuration</span></span>

<span data-ttu-id="685ce-213">Si su configuración de CHAP es incorrecta, es probable que toosee una **error de autenticación** mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="685ce-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="685ce-214">Verificación de la configuración de CHAP</span><span class="sxs-lookup"><span data-stu-id="685ce-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="685ce-215">Puede comprobar que CHAP se esté usando siguiendo los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="685ce-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="685ce-216">tooverify su configuración de CHAP</span><span class="sxs-lookup"><span data-stu-id="685ce-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="685ce-217">Haga clic en **Destinos favoritos**.</span><span class="sxs-lookup"><span data-stu-id="685ce-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="685ce-218">Seleccione el destino de hello para el que ha habilitado la autenticación.</span><span class="sxs-lookup"><span data-stu-id="685ce-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="685ce-219">Haga clic en **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="685ce-219">Click **Details**.</span></span>
   
    ![Destinos favoritos de las propiedades del iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="685ce-221">Hola **detalles de destino favorito** cuadro de diálogo Entrada de nota Hola Hola **autenticación** campo.</span><span class="sxs-lookup"><span data-stu-id="685ce-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="685ce-222">Si la configuración de hello sea correcta, debe indicar **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="685ce-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Detalles de destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="685ce-224">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="685ce-224">Next steps</span></span>

* <span data-ttu-id="685ce-225">Obtenga más información acerca de la [Seguridad de StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="685ce-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="685ce-226">Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="685ce-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

