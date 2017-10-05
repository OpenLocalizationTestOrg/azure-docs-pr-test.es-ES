---
title: "Información sobre errores de WebHCat y resolución en HDInsight y Azure | Microsoft Docs"
description: "Aprenda cómo tratar errores comunes devueltos por WebHCat en HDInsight y cómo resolverlos."
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
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="149c4-103">Entender y resolver errores recibidos de WebHCat en HDInsight</span><span class="sxs-lookup"><span data-stu-id="149c4-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="149c4-104">Obtener información acerca de los errores recibidos al utilizar WebHCat con HDInsight y cómo resolverlos.</span><span class="sxs-lookup"><span data-stu-id="149c4-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="149c4-105">Las herramientas de cliente como Azure PowerShell y Data Lake Tools para Visual Studio usan WebHCat internamente.</span><span class="sxs-lookup"><span data-stu-id="149c4-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="149c4-106">¿Qué es WebHCat?</span><span class="sxs-lookup"><span data-stu-id="149c4-106">What is WebHCat</span></span>

<span data-ttu-id="149c4-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) es una API de REST para [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), una capa de administración de almacenamiento y tablas para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="149c4-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="149c4-108">WebHCat está habilitado de manera predeterminada en los clústeres de HDInsight y se usa por diversas herramientas para enviar trabajos, obtener el estado de los trabajos, etc. sin iniciar sesión en el clúster.</span><span class="sxs-lookup"><span data-stu-id="149c4-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="149c4-109">Modificación de la configuración</span><span class="sxs-lookup"><span data-stu-id="149c4-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="149c4-110">Algunos de los errores que se muestran en este documento se producen porque se ha superado un máximo configurado.</span><span class="sxs-lookup"><span data-stu-id="149c4-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="149c4-111">Cuando el paso de la resolución menciona que puede cambiar un valor, debe usar una de las acciones siguientes para realizar el cambio:</span><span class="sxs-lookup"><span data-stu-id="149c4-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="149c4-112">Para clústeres de **Windows** : use una acción de script para configurar el valor durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="149c4-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="149c4-113">Para obtener más información, vea [Desarrollar acciones de script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="149c4-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="149c4-114">Para clústeres **Linux** : use Ambari (web o API de REST) para modificar el valor.</span><span class="sxs-lookup"><span data-stu-id="149c4-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="149c4-115">Para obtener más información, vea [Administrar HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="149c4-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="149c4-116">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="149c4-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="149c4-117">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="149c4-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="149c4-118">Configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="149c4-118">Default configuration</span></span>

<span data-ttu-id="149c4-119">Si se superan los siguientes valores predeterminados, puede degradar el rendimiento de WebHCat o provocar errores:</span><span class="sxs-lookup"><span data-stu-id="149c4-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="149c4-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="149c4-120">Setting</span></span> | <span data-ttu-id="149c4-121">Qué hace</span><span class="sxs-lookup"><span data-stu-id="149c4-121">What it does</span></span> | <span data-ttu-id="149c4-122">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="149c4-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="149c4-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="149c4-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="149c4-124">El número máximo de trabajos que pueden estar activos de manera simultánea (pendientes o en ejecución)</span><span class="sxs-lookup"><span data-stu-id="149c4-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="149c4-125">10.000</span><span class="sxs-lookup"><span data-stu-id="149c4-125">10,000</span></span> |
| <span data-ttu-id="149c4-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="149c4-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="149c4-127">El número máximo de solicitudes que se pueden atender de manera simultánea</span><span class="sxs-lookup"><span data-stu-id="149c4-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="149c4-128">20</span><span class="sxs-lookup"><span data-stu-id="149c4-128">20</span></span> |
| <span data-ttu-id="149c4-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="149c4-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="149c4-130">El número de días que se conservará el historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="149c4-130">The number of days that job history are retained</span></span> |<span data-ttu-id="149c4-131">7 días</span><span class="sxs-lookup"><span data-stu-id="149c4-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="149c4-132">Demasiadas solicitudes</span><span class="sxs-lookup"><span data-stu-id="149c4-132">Too many requests</span></span>

<span data-ttu-id="149c4-133">**Código de estado HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="149c4-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="149c4-134">Causa</span><span class="sxs-lookup"><span data-stu-id="149c4-134">Cause</span></span> | <span data-ttu-id="149c4-135">Resolución</span><span class="sxs-lookup"><span data-stu-id="149c4-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="149c4-136">Ha superado el máximo de solicitudes simultáneas atendidas por WebHCat por minuto (el valor predeterminado es 20).</span><span class="sxs-lookup"><span data-stu-id="149c4-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="149c4-137">Reduzca la carga de trabajo para asegurarse de que no envía más que el número máximo de solicitudes simultáneas o aumente el límite de solicitudes simultáneas modificando `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="149c4-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="149c4-138">Consulte [Modificación de la configuración](#modifying-configuration) para más información.</span><span class="sxs-lookup"><span data-stu-id="149c4-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="149c4-139">Servidor no disponible</span><span class="sxs-lookup"><span data-stu-id="149c4-139">Server unavailable</span></span>

<span data-ttu-id="149c4-140">**Código de estado HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="149c4-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="149c4-141">Causa</span><span class="sxs-lookup"><span data-stu-id="149c4-141">Cause</span></span> | <span data-ttu-id="149c4-142">Resolución</span><span class="sxs-lookup"><span data-stu-id="149c4-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="149c4-143">Este código de estado suele producirse durante la conmutación por error entre el nodo principal primario y secundario para el clúster.</span><span class="sxs-lookup"><span data-stu-id="149c4-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="149c4-144">Espere dos minutos y vuelva a intentar la operación.</span><span class="sxs-lookup"><span data-stu-id="149c4-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="149c4-145">Contenido de solicitud incorrecta: no se encontró el trabajo.</span><span class="sxs-lookup"><span data-stu-id="149c4-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="149c4-146">**Código de estado HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="149c4-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="149c4-147">Causa</span><span class="sxs-lookup"><span data-stu-id="149c4-147">Cause</span></span> | <span data-ttu-id="149c4-148">Resolución</span><span class="sxs-lookup"><span data-stu-id="149c4-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="149c4-149">Los detalles de los trabajos se han limpiado con el limpiador del historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="149c4-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="149c4-150">El período de retención predeterminado para el historial de trabajos es de 7 días.</span><span class="sxs-lookup"><span data-stu-id="149c4-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="149c4-151">El período de retención predeterminado puede cambiarse modificando `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="149c4-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="149c4-152">Consulte [Modificación de la configuración](#modifying-configuration) para más información.</span><span class="sxs-lookup"><span data-stu-id="149c4-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="149c4-153">Se ha suprimido el trabajo debido a una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="149c4-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="149c4-154">Vuelva a intentar el envío de trabajos durante un tiempo máximo de dos minutos</span><span class="sxs-lookup"><span data-stu-id="149c4-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="149c4-155">Se usó un identificador de trabajo no válido</span><span class="sxs-lookup"><span data-stu-id="149c4-155">An Invalid job id was used</span></span> |<span data-ttu-id="149c4-156">Compruebe si el id. de trabajo es correcto</span><span class="sxs-lookup"><span data-stu-id="149c4-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="149c4-157">Puerta de enlace incorrecta</span><span class="sxs-lookup"><span data-stu-id="149c4-157">Bad gateway</span></span>

<span data-ttu-id="149c4-158">**Código de estado HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="149c4-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="149c4-159">Causa</span><span class="sxs-lookup"><span data-stu-id="149c4-159">Cause</span></span> | <span data-ttu-id="149c4-160">Resolución</span><span class="sxs-lookup"><span data-stu-id="149c4-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="149c4-161">La recolección de elementos no utilizados internos se está produciendo en el proceso de WebHCat</span><span class="sxs-lookup"><span data-stu-id="149c4-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="149c4-162">Espere a que termine la recolección de elementos no utilizados o reinicie el servicio de WebHCat</span><span class="sxs-lookup"><span data-stu-id="149c4-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="149c4-163">Tiempo de espera de una respuesta desde el servicio de ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="149c4-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="149c4-164">Este error se puede producir cuando el número de aplicaciones activas alcanza el máximo configurado (el valor predeterminado es 10.000)</span><span class="sxs-lookup"><span data-stu-id="149c4-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="149c4-165">Espere a que finalice los trabajos actualmente en ejecución o aumente el límite de trabajos simultáneos modificando `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="149c4-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="149c4-166">Consulte [Modificación de la configuración](#modifying-configuration) para más información.</span><span class="sxs-lookup"><span data-stu-id="149c4-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="149c4-167">Al intentar recuperar todos los trabajos a través de la llamada [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) mientras `Fields` está establecido en `*`</span><span class="sxs-lookup"><span data-stu-id="149c4-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="149c4-168">No recupere *todos* los detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="149c4-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="149c4-169">En su lugar, use `jobid` para recuperar detalles de trabajos solo mayores que un id. de trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="149c4-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="149c4-170">O bien, no use `Fields`</span><span class="sxs-lookup"><span data-stu-id="149c4-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="149c4-171">El servicio de WebHCat está inactivo durante la conmutación por error del nodo principal</span><span class="sxs-lookup"><span data-stu-id="149c4-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="149c4-172">Espere dos minutos y vuelva a intentar la operación</span><span class="sxs-lookup"><span data-stu-id="149c4-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="149c4-173">Hay más de 500 trabajos pendientes enviados a través de WebHCat</span><span class="sxs-lookup"><span data-stu-id="149c4-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="149c4-174">Espere hasta que hayan finalizado los trabajos pendientes actualmente antes de enviar más trabajos</span><span class="sxs-lookup"><span data-stu-id="149c4-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
