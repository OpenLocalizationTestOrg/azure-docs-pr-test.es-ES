---
title: aaaUnderstand y resuelva los errores de WebHCat en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooabout los errores comunes devuelven por WebHCat de HDInsight y cómo tooresolve ellos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="0b70c-103">Entender y resolver errores recibidos de WebHCat en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b70c-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="0b70c-104">Obtenga información acerca de los errores recibidos al usar WebHCat con HDInsight y cómo tooresolve ellos.</span><span class="sxs-lookup"><span data-stu-id="0b70c-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="0b70c-105">WebHCat se usa internamente por herramientas de cliente, como PowerShell de Azure y Hola Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b70c-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="0b70c-106">¿Qué es WebHCat?</span><span class="sxs-lookup"><span data-stu-id="0b70c-106">What is WebHCat</span></span>

<span data-ttu-id="0b70c-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) es una API de REST para [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), una capa de administración de almacenamiento y tablas para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0b70c-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="0b70c-108">WebHCat está habilitada de forma predeterminada en los clústeres de HDInsight y usa varios trabajos de toosubmit de herramientas, obtener el estado del trabajo, etc. sin iniciar sesión en el clúster de toohello.</span><span class="sxs-lookup"><span data-stu-id="0b70c-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="0b70c-109">Modificación de la configuración</span><span class="sxs-lookup"><span data-stu-id="0b70c-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b70c-110">Algunos de los errores de hello indicados en este documento se producen porque se ha superado el máximo configurado.</span><span class="sxs-lookup"><span data-stu-id="0b70c-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="0b70c-111">Cuando los pasos de resolución de hello mencionan que puede cambiar un valor, debe utilizar uno de hello siguiente tooperform Hola cambio:</span><span class="sxs-lookup"><span data-stu-id="0b70c-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="0b70c-112">Para **Windows** clústeres: usar un valor de Hola de tooconfigure de acción de secuencia de comandos durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="0b70c-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="0b70c-113">Para obtener más información, vea [Desarrollar acciones de script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="0b70c-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="0b70c-114">Para **Linux** clústeres: valor de hello toomodify Ambari de uso (web o API de REST).</span><span class="sxs-lookup"><span data-stu-id="0b70c-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="0b70c-115">Para obtener más información, vea [Administrar HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="0b70c-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b70c-116">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="0b70c-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0b70c-117">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0b70c-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="0b70c-118">Configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="0b70c-118">Default configuration</span></span>

<span data-ttu-id="0b70c-119">Si se supera Hola siguiendo los valores predeterminados, puede degradar el rendimiento de WebHCat o provocar errores:</span><span class="sxs-lookup"><span data-stu-id="0b70c-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="0b70c-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="0b70c-120">Setting</span></span> | <span data-ttu-id="0b70c-121">Qué hace</span><span class="sxs-lookup"><span data-stu-id="0b70c-121">What it does</span></span> | <span data-ttu-id="0b70c-122">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="0b70c-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b70c-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="0b70c-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="0b70c-124">Hola número máximo de trabajos que pueden estar activas simultáneamente (pendiente o en ejecución)</span><span class="sxs-lookup"><span data-stu-id="0b70c-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="0b70c-125">10.000</span><span class="sxs-lookup"><span data-stu-id="0b70c-125">10,000</span></span> |
| <span data-ttu-id="0b70c-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="0b70c-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="0b70c-127">número máximo de Hola de solicitudes que puede servir de forma simultánea</span><span class="sxs-lookup"><span data-stu-id="0b70c-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="0b70c-128">20 |</span><span class="sxs-lookup"><span data-stu-id="0b70c-128">20</span></span> |
| <span data-ttu-id="0b70c-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="0b70c-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="0b70c-130">Hola número de días que el historial de trabajos que se conservarán</span><span class="sxs-lookup"><span data-stu-id="0b70c-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="0b70c-131">7 días</span><span class="sxs-lookup"><span data-stu-id="0b70c-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="0b70c-132">Demasiadas solicitudes</span><span class="sxs-lookup"><span data-stu-id="0b70c-132">Too many requests</span></span>

<span data-ttu-id="0b70c-133">**Código de estado HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="0b70c-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="0b70c-134">Causa</span><span class="sxs-lookup"><span data-stu-id="0b70c-134">Cause</span></span> | <span data-ttu-id="0b70c-135">Resolución</span><span class="sxs-lookup"><span data-stu-id="0b70c-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0b70c-136">Se ha superado Hola máximo de solicitudes simultáneas atendido por WebHCat por minuto (el valor predeterminado es 20)</span><span class="sxs-lookup"><span data-stu-id="0b70c-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="0b70c-137">Reducir el tooensure de carga de trabajo que no enviar más de número máximo de solicitudes simultáneas de Hola o aumentar el límite de solicitudes simultáneas de hello modificando `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="0b70c-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="0b70c-138">Consulte [Modificación de la configuración](#modifying-configuration) para más información.</span><span class="sxs-lookup"><span data-stu-id="0b70c-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="0b70c-139">Servidor no disponible</span><span class="sxs-lookup"><span data-stu-id="0b70c-139">Server unavailable</span></span>

<span data-ttu-id="0b70c-140">**Código de estado HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="0b70c-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="0b70c-141">Causa</span><span class="sxs-lookup"><span data-stu-id="0b70c-141">Cause</span></span> | <span data-ttu-id="0b70c-142">Resolución</span><span class="sxs-lookup"><span data-stu-id="0b70c-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0b70c-143">Este código de estado se produce normalmente durante la conmutación por error entre Hola principal y secundaria nodo principal para el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="0b70c-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="0b70c-144">Espere dos minutos y vuelva a intentar la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="0b70c-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="0b70c-145">Contenido de solicitud incorrecta: no se encontró el trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b70c-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="0b70c-146">**Código de estado HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="0b70c-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="0b70c-147">Causa</span><span class="sxs-lookup"><span data-stu-id="0b70c-147">Cause</span></span> | <span data-ttu-id="0b70c-148">Resolución</span><span class="sxs-lookup"><span data-stu-id="0b70c-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0b70c-149">Detalles del trabajo se han limpiado por historial de trabajos de hello limpiador</span><span class="sxs-lookup"><span data-stu-id="0b70c-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="0b70c-150">período de retención predeterminado de Hello para el historial de trabajos es 7 días.</span><span class="sxs-lookup"><span data-stu-id="0b70c-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="0b70c-151">período de retención de Hello predeterminado puede cambiarse modificando `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="0b70c-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="0b70c-152">Consulte [Modificación de la configuración](#modifying-configuration) para más información.</span><span class="sxs-lookup"><span data-stu-id="0b70c-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="0b70c-153">Se ha suprimido el trabajo debido a tooa conmutación por error</span><span class="sxs-lookup"><span data-stu-id="0b70c-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="0b70c-154">Vuelva a intentar el envío de trabajos para la tootwo minutos</span><span class="sxs-lookup"><span data-stu-id="0b70c-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="0b70c-155">Se usó un identificador de trabajo no válido</span><span class="sxs-lookup"><span data-stu-id="0b70c-155">An Invalid job id was used</span></span> |<span data-ttu-id="0b70c-156">Compruebe si el Id. de trabajo de hello es correcto</span><span class="sxs-lookup"><span data-stu-id="0b70c-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="0b70c-157">Puerta de enlace incorrecta</span><span class="sxs-lookup"><span data-stu-id="0b70c-157">Bad gateway</span></span>

<span data-ttu-id="0b70c-158">**Código de estado HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="0b70c-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="0b70c-159">Causa</span><span class="sxs-lookup"><span data-stu-id="0b70c-159">Cause</span></span> | <span data-ttu-id="0b70c-160">Resolución</span><span class="sxs-lookup"><span data-stu-id="0b70c-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0b70c-161">Recolección de elementos internos se está produciendo en hello WebHCat proceso</span><span class="sxs-lookup"><span data-stu-id="0b70c-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="0b70c-162">Espere toofinish de la colección de elementos no utilizados o reiniciar el servicio WebHCat de Hola</span><span class="sxs-lookup"><span data-stu-id="0b70c-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="0b70c-163">Tiempo de espera esperando una respuesta de hello servicio ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="0b70c-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="0b70c-164">Este error puede producirse cuando sale de número de Hola de aplicaciones activas máximo Hola configurado (el valor predeterminado es 10.000)</span><span class="sxs-lookup"><span data-stu-id="0b70c-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="0b70c-165">Espere a que se está ejecutando trabajos toocomplete o aumentar el límite de trabajos simultáneos de hello modificando `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="0b70c-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="0b70c-166">Para obtener más información, vea hello [modificar configuración](#modifying-configuration) sección.</span><span class="sxs-lookup"><span data-stu-id="0b70c-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="0b70c-167">Intentar tooretrieve todos los trabajos a través de hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) llamada mientras `Fields` se establece demasiado`*`</span><span class="sxs-lookup"><span data-stu-id="0b70c-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="0b70c-168">No recupere *todos* los detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b70c-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="0b70c-169">En su lugar use `jobid` tooretrieve detalles para trabajos mayores sólo a determinados Id. de trabajo. O bien, no use `Fields`</span><span class="sxs-lookup"><span data-stu-id="0b70c-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="0b70c-170">Hola servicio WebHCat está inactivo durante la conmutación por error de nodo principal</span><span class="sxs-lookup"><span data-stu-id="0b70c-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="0b70c-171">Espere dos minutos y vuelva a intentar la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="0b70c-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="0b70c-172">Hay más de 500 trabajos pendientes enviados a través de WebHCat</span><span class="sxs-lookup"><span data-stu-id="0b70c-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="0b70c-173">Espere hasta que hayan finalizado los trabajos pendientes actualmente antes de enviar más trabajos</span><span class="sxs-lookup"><span data-stu-id="0b70c-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
