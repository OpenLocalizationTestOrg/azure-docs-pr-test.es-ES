---
title: aaaConfigure CHAP para el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo tooconfigure Hola protocolo de autenticación por desafío mutuo (CHAP) en un dispositivo de StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="f3b46-103">Configurar CHAP para el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="f3b46-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="f3b46-104">Este tutorial le explica cómo tooconfigure CHAP para el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f3b46-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="f3b46-105">procedimiento de Hello detallado en este artículo aplica 8000 serie de tooStorSimple, así como dispositivos de StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="f3b46-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="f3b46-106">CHAP significa Protocolo de autenticación por desafío mutuo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="f3b46-107">Es un esquema de autenticación usado por identidad de hello toovalidate de servidores de clientes remotos.</span><span class="sxs-lookup"><span data-stu-id="f3b46-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="f3b46-108">comprobación de Hola se basa en una contraseña compartida o un secreto.</span><span class="sxs-lookup"><span data-stu-id="f3b46-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="f3b46-109">CHAP puede ser unidireccional o mutuo (bidireccional).</span><span class="sxs-lookup"><span data-stu-id="f3b46-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="f3b46-110">CHAP unidireccional es cuando el destino de hello autentica como iniciador.</span><span class="sxs-lookup"><span data-stu-id="f3b46-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="f3b46-111">CHAP bidireccional o mutuo, en hello otra parte, requiere que el destino de hello autentique el iniciador de hello y, a continuación, el iniciador de hello autenticar destino Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="f3b46-112">La autenticación del iniciador puede implementarse sin la autenticación del destino.</span><span class="sxs-lookup"><span data-stu-id="f3b46-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="f3b46-113">Sin embargo, la autenticación del destino solo puede implementarse si también se implementa la autenticación del iniciador.</span><span class="sxs-lookup"><span data-stu-id="f3b46-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="f3b46-114">Como práctica recomendada, se recomienda que utilice la seguridad CHAP tooenhance iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f3b46-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b46-115">Tenga en cuenta que los dispositivos StorSimple no admiten IPSEC actualmente.</span><span class="sxs-lookup"><span data-stu-id="f3b46-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="f3b46-116">configuración de CHAP Hello en dispositivo de StorSimple de hello puede configurarse en hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="f3b46-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="f3b46-117">Autenticación unidireccional</span><span class="sxs-lookup"><span data-stu-id="f3b46-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="f3b46-118">Autenticación bidireccional o mutua o inversa</span><span class="sxs-lookup"><span data-stu-id="f3b46-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="f3b46-119">En cada uno de estos casos, el portal de Hola para dispositivo de Hola y el software del iniciador de iSCSI de hello server necesita toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="f3b46-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="f3b46-120">Hello pasos detallados para esta configuración se describen en hello siguiendo el tutorial.</span><span class="sxs-lookup"><span data-stu-id="f3b46-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="f3b46-121">Autenticación unidireccional</span><span class="sxs-lookup"><span data-stu-id="f3b46-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="f3b46-122">En la autenticación unidireccional, destino Hola autentica el iniciador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="f3b46-123">Esta autenticación requiere que configure valores del iniciador de CHAP hello en dispositivo de StorSimple de Hola y Hola iSCSI software Initiator en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="f3b46-124">Hola procedimientos detallados para el dispositivo StorSimple y host de Windows se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="f3b46-125">tooconfigure el dispositivo para la autenticación unidireccional</span><span class="sxs-lookup"><span data-stu-id="f3b46-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="f3b46-126">En el portal de Azure clásico en Hola Hola **dispositivos** página, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="f3b46-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Iniciador de CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="f3b46-128">Desplácese hacia abajo en esta página y en hello **iniciador CHAP** sección:</span><span class="sxs-lookup"><span data-stu-id="f3b46-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="f3b46-129">Proporcione un nombre de usuario para su iniciador de CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3b46-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="f3b46-130">Proporcionar una contraseña para su iniciador de CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3b46-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="f3b46-131">nombre de usuario CHAP Hola debe contener menos de 233 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f3b46-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="f3b46-132">Contraseña CHAP de Hello debe tener entre 12 y 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f3b46-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="f3b46-133">Un nombre de usuario o una contraseña más larga se producirá un error de autenticación en el host de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f3b46-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="f3b46-134">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-134">Confirm hello password.</span></span>
3. <span data-ttu-id="f3b46-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-135">Click **Save**.</span></span> <span data-ttu-id="f3b46-136">Aparecerá un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="f3b46-137">Haga clic en **Aceptar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="f3b46-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="f3b46-138">servidor de host tooconfigure autenticación unidireccional en Windows hello</span><span class="sxs-lookup"><span data-stu-id="f3b46-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="f3b46-139">En el servidor de host de Windows hello, inicie el iniciador iSCSI de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="f3b46-140">Hola **propiedades del iniciador iSCSI** ventana, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f3b46-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="f3b46-141">Haga clic en hello **detección** ficha.</span><span class="sxs-lookup"><span data-stu-id="f3b46-141">Click hello **Discovery** tab.</span></span>
      
       ![Propiedades del iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="f3b46-143">Haga clic en **Detectar portal**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="f3b46-144">Hola **detectar Portal de destino** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="f3b46-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="f3b46-145">Especifique la dirección IP de hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="f3b46-146">Haga clic en **Avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-146">Click **Advanced**.</span></span>
      
       ![Detectar portal de destino](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="f3b46-148">Hola **configuración avanzada** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="f3b46-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="f3b46-149">Seleccione hello **inicio de sesión habilitar CHAP** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="f3b46-150">Hola **nombre** campo, nombre de usuario de Hola de fuente de alimentación que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="f3b46-151">Hola **secreto de destino** campo, una fuente de alimentación Hola contraseña que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="f3b46-152">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-152">Click **OK**.</span></span>
      
       ![General - Configuración avanzada](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="f3b46-154">En hello **destinos** ficha de hello **propiedades del iniciador iSCSI** ventana, el estado del dispositivo Hola debe aparecer como **conectado**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="f3b46-155">Si usa un dispositivo StorSimple 1200, cada volumen se montará como un destino iSCSI como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="f3b46-156">Por lo tanto, los pasos 3 y 4 será necesario toobe repite para cada volumen.</span><span class="sxs-lookup"><span data-stu-id="f3b46-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volúmenes montados como destinos independientes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="f3b46-158">Si cambia el nombre de iSCSI de hello, se usará el nuevo nombre de Hola para nuevas sesiones de iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f3b46-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="f3b46-159">La nueva configuración no se utiliza para las sesiones existentes hasta que cierra sesión y vuelve a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="f3b46-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="f3b46-160">Para obtener más información sobre cómo configurar CHAP en el servidor de host de Windows hello, vaya demasiado[consideraciones adicionales](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="f3b46-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="f3b46-161">Autenticación bidireccional o mutua</span><span class="sxs-lookup"><span data-stu-id="f3b46-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="f3b46-162">En la autenticación bidireccional, destino de hello autentica el iniciador de hello y, a continuación, iniciador Hola autentica destino Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="f3b46-163">Esto requiere valores del iniciador CHAP de hello usuario tooconfigure hello, así como Hola invertir la configuración de CHAP en dispositivo de Hola y software en el host de hello del iniciador iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f3b46-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="f3b46-164">Hello procedimientos siguientes describen la autenticación mutua de hello pasos tooconfigure en el dispositivo de Hola y en el host de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f3b46-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="f3b46-165">tooconfigure el dispositivo para la autenticación mutua</span><span class="sxs-lookup"><span data-stu-id="f3b46-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="f3b46-166">En el portal de Azure clásico en Hola Hola **dispositivos** página, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="f3b46-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Destino de CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="f3b46-168">Desplácese hacia abajo en esta página y en hello **destino CHAP** sección:</span><span class="sxs-lookup"><span data-stu-id="f3b46-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="f3b46-169">Proporcione un **Nombre de usuario de CHAP inverso** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="f3b46-170">Proporcione una **Contraseña de CHAP inverso** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="f3b46-171">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-171">Confirm hello password.</span></span>
3. <span data-ttu-id="f3b46-172">Hola **iniciador CHAP** sección:</span><span class="sxs-lookup"><span data-stu-id="f3b46-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="f3b46-173">Proporcione un **nombre de usuario** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="f3b46-174">Proporcione una **contraseña** para su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="f3b46-175">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-175">Confirm hello password.</span></span>
4. <span data-ttu-id="f3b46-176">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-176">Click **Save**.</span></span> <span data-ttu-id="f3b46-177">Aparecerá un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="f3b46-178">Haga clic en **Aceptar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="f3b46-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="f3b46-179">servidor de host de la autenticación bidireccional tooconfigure en Windows hello</span><span class="sxs-lookup"><span data-stu-id="f3b46-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="f3b46-180">En el servidor de host de Windows hello, inicie el iniciador iSCSI de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="f3b46-181">Hola **propiedades del iniciador iSCSI** ventana, haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="f3b46-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="f3b46-182">Haga clic en **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="f3b46-183">Hola **secreto CHAP mutuo del iniciador iSCSI** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="f3b46-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="f3b46-184">Hola de tipo **contraseña de CHAP inverso** que configuró en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="f3b46-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="f3b46-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-185">Click **OK**.</span></span>
      
       ![Secreto CHAP mutuo del iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="f3b46-187">Haga clic en hello **destinos** ficha.</span><span class="sxs-lookup"><span data-stu-id="f3b46-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="f3b46-188">Haga clic en hello **conectar** botón.</span><span class="sxs-lookup"><span data-stu-id="f3b46-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="f3b46-189">Hola **conectar tooTarget** cuadro de diálogo, haga clic en **avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="f3b46-190">Hola **propiedades avanzadas** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="f3b46-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="f3b46-191">Seleccione hello **inicio de sesión habilitar CHAP** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="f3b46-192">Hola **nombre** campo, nombre de usuario de Hola de fuente de alimentación que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="f3b46-193">Hola **secreto de destino** campo, una fuente de alimentación Hola contraseña que especificó para hello iniciador de CHAP en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="f3b46-194">Seleccione hello **realizar autenticación mutua** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Autenticación mutua de configuración avanzada](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="f3b46-196">Haga clic en **Aceptar** configuración de CHAP hello toocomplete</span><span class="sxs-lookup"><span data-stu-id="f3b46-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="f3b46-197">Para obtener más información sobre cómo configurar CHAP en el servidor de host de Windows hello, vaya demasiado[consideraciones adicionales](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="f3b46-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="f3b46-198">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="f3b46-198">Additional considerations</span></span>
<span data-ttu-id="f3b46-199">Hola **conexión rápida** característica no admite conexiones con CHAP habilitado.</span><span class="sxs-lookup"><span data-stu-id="f3b46-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="f3b46-200">Cuando CHAP esté habilitado, asegúrese de que utiliza hello **conectar** botón que está disponible en hello **destinos** destino de tooa tooconnect de pestaña.</span><span class="sxs-lookup"><span data-stu-id="f3b46-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Conectar tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="f3b46-202">Hola **conectar tooTarget** cuadro de diálogo es hello presentan, seleccione **agregar esta lista de toohello de conexión de destinos favoritos** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="f3b46-203">Esto garantiza que cada vez que se reinicie el equipo de hello, se realiza un intento toorestore Hola conexión toohello favoritos los destinos iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f3b46-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="f3b46-204">Errores durante la configuración</span><span class="sxs-lookup"><span data-stu-id="f3b46-204">Errors during configuration</span></span>
<span data-ttu-id="f3b46-205">Si su configuración de CHAP es incorrecta, es probable que toosee una **error de autenticación** mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="f3b46-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="f3b46-206">Verificación de la configuración de CHAP</span><span class="sxs-lookup"><span data-stu-id="f3b46-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="f3b46-207">Puede comprobar que CHAP se esté usando siguiendo los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3b46-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="f3b46-208">tooverify su configuración de CHAP</span><span class="sxs-lookup"><span data-stu-id="f3b46-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="f3b46-209">Haga clic en **Destinos favoritos**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="f3b46-210">Seleccione el destino de hello para el que ha habilitado la autenticación.</span><span class="sxs-lookup"><span data-stu-id="f3b46-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="f3b46-211">Haga clic en **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-211">Click **Details**.</span></span>
   
    ![Destinos favoritos de las propiedades del iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="f3b46-213">Hola **detalles de destino favorito** cuadro de diálogo Entrada de nota Hola Hola **autenticación** campo.</span><span class="sxs-lookup"><span data-stu-id="f3b46-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="f3b46-214">Si la configuración de hello sea correcta, debe indicar **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="f3b46-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Detalles de destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="f3b46-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3b46-216">Next steps</span></span>
* <span data-ttu-id="f3b46-217">Obtenga más información acerca de la [Seguridad de StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="f3b46-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="f3b46-218">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f3b46-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

