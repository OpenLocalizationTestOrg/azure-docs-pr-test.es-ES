---
title: "aaaNAMD con Microsoft HPC Pack en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Implementación de un clúster de Microsoft HPC Pack en Azure y ejecución de una simulación de NAMD con charmrun en varios nodos de proceso de Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="ddeb8-103">Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="ddeb8-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="ddeb8-104">Este artículo muestra una manera de toorun una carga de trabajo de informática de alto rendimiento (HPC) de Linux en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="ddeb8-105">En este caso, configure un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) de Cluster Server en Azure con nodos de proceso de Linux y ejecutar un [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate de simulación y visualizar la estructura de Hola de un sistema grande biomoleculares.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="ddeb8-106">**NAMD** (para el programa de Dynamics Molecular Nanoscale) es un paquete de dynamics molecular paralelo diseñado para simulación de alto rendimiento de los sistemas de gran tamaño biomoleculares que contiene una toomillions de subcomponentes.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="ddeb8-107">Algunos ejemplos de estos sistemas son virus, estructuras celulares y proteínas grandes.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="ddeb8-108">NAMD escala toohundreds de núcleos para simulaciones típicos y toomore a 500.000 núcleos para simulaciones de hello más grandes.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="ddeb8-109">**Microsoft HPC Pack** proporciona características toorun HPC a gran escala y aplicaciones en paralelo en clústeres de equipos locales o máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="ddeb8-110">HPC Pack, que se desarrolló originalmente como una solución para cargas de trabajo de Windows HPC, ahora admite la ejecución de las aplicaciones HPC Linux en máquinas virtuales de nodos de proceso de Linux implementadas en un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="ddeb8-111">Consulte [Introducción a los nodos de ejecución de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para obtener información.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="ddeb8-112">Para otro toorun opciones Linux HPC cargas de trabajo en Azure, consulte [recursos técnicos para el lote e informática de alto rendimiento](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddeb8-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ddeb8-113">Prerequisites</span></span>
* <span data-ttu-id="ddeb8-114">**Clúster de HPC Pack con nodos de ejecución de Linux**: implemente un clúster de HPC Pack con nodos de proceso de Linux en Azure utilizando una [plantilla de Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o un [script de Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="ddeb8-115">Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para requisitos previos de Hola y pasos para cualquiera de las opciones.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="ddeb8-116">Si elige Hola opción de implementación de secuencia de comandos de PowerShell, vea el archivo de configuración de ejemplo de Hola en archivos de ejemplo de Hola final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="ddeb8-117">Este archivo configura un clúster basado en Azure HPC Pack que consta de un nodo principal de Windows Server 2012 R2 y cuatro nodos de ejecución de tamaño grande CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="ddeb8-118">Adapte este archivo según las necesidades de su entorno.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="ddeb8-119">**Archivos de software y un tutorial NAMD** -software NAMD descargar para Linux de hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) sitio (es necesario registrarse).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="ddeb8-120">En este artículo se basa en NAMD versión 2.10 y usa hello [x86_64 de Linux (64-bit Intel o AMD con Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="ddeb8-121">Descargar hello [archivos del tutorial NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="ddeb8-122">descargas de Hello son archivos .tar y necesita un archivos de Windows herramienta tooextract hello en el nodo principal del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="ddeb8-123">archivos de hello tooextract, siga las instrucciones de hello más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="ddeb8-124">**VMD** (opcional): resultados de hello toosee de su trabajo NAMD, descargue e instale programas de visualización molecular hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) en un equipo de su elección.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="ddeb8-125">versión actual de Hello es 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="ddeb8-126">Vea Hola VMD descargar tooget de sitio que se inició.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="ddeb8-127">Configuración de la confianza mutua entre nodos de proceso</span><span class="sxs-lookup"><span data-stu-id="ddeb8-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="ddeb8-128">Ejecutar un trabajo de entre nodos en varios nodos de Linux requiere Hola nodos tootrust entre sí (por **rsh** o **ssh**).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="ddeb8-129">Cuando se crea el clúster de HPC Pack Hola con hello script de implementación de Microsoft HPC Pack IaaS, script de Hola configura automáticamente una confianza mutua permanente para cuenta de administrador de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="ddeb8-130">Para crear en el dominio del clúster de Hola de los usuarios sin privilegios de administrador, deberá tooset temporal confianza mutua entre los nodos de hello cuando un trabajo se asigna a toothem.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="ddeb8-131">A continuación, destruir relación Hola una vez completado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="ddeb8-132">toodo esto para cada usuario, proporcione un clúster de toohello del par de claves de RSA que HPC Pack utiliza la relación de confianza de tooestablish Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="ddeb8-133">A continuación figuran las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="ddeb8-134">Generación de un par de claves RSA</span><span class="sxs-lookup"><span data-stu-id="ddeb8-134">Generate an RSA key pair</span></span>
<span data-ttu-id="ddeb8-135">Resulta fácil toogenerate un par de claves de RSA, que contiene una clave pública y una clave privada y, a continuación, ejecutando Hola Linux **ssh-keygen** comando.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="ddeb8-136">Inicie sesión en tooa equipo Linux.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="ddeb8-137">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="ddeb8-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="ddeb8-138">Presione **ENTRAR** toouse Hola predeterminados hasta que se complete el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="ddeb8-139">No escriba aquí una frase de contraseña. Cuando se le pida una contraseña, solo tiene que presionar **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generación de un par de claves RSA][keygen]
3. <span data-ttu-id="ddeb8-141">Cambie el directorio toohello ~/.ssh directorio.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="ddeb8-142">clave privada de Hola se almacena en la clave pública de hello y id_rsa en id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Claves públicas y privadas][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="ddeb8-144">Agregar clúster de HPC Pack en toohello Hola par de claves</span><span class="sxs-lookup"><span data-stu-id="ddeb8-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="ddeb8-145">[Conectarse mediante Escritorio remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo principal VM con Hola credenciales de dominio que ha proporcionado al implementar el clúster de hello (por ejemplo, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="ddeb8-146">Administrar clústeres de Hola desde el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="ddeb8-147">Utilice toocreate estándar de procedimientos de Windows Server una cuenta de usuario de dominio dominio del clúster de hello de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="ddeb8-148">Por ejemplo, usar hello usuario de Active Directory y la herramienta de equipos en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="ddeb8-149">ejemplos de Hello en este artículo se supone que crea un usuario de dominio denominado hpcuser en el dominio de hello hpclab (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="ddeb8-150">Agregar clúster de HPC Pack de toohello de usuario de dominio de Hola como un usuario del clúster.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="ddeb8-151">Para obtener instrucciones, consulte [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx)(Adición o eliminación de usuarios de clúster).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="ddeb8-152">Cree un archivo denominado C:\cred.xml y copiar datos de clave de RSA de hello en él.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="ddeb8-153">Puede encontrar un ejemplo de Hola archivos de ejemplo al final de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="ddeb8-154">Abra un símbolo del sistema y escriba el siguiente comando hello tooset credenciales datos para hello hpclab\hpcuser cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="ddeb8-155">Usar hello **extendeddata** toopass parámetro Hola nombre del archivo de C:\cred.xml Hola que creó para los datos clave Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="ddeb8-156">Este comando se completa correctamente sin salida.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-156">This command completes successfully without output.</span></span> <span data-ttu-id="ddeb8-157">Después de establecer las credenciales de Hola Hola para cuentas de usuario que necesita toorun trabajos, almacenar el archivo de cred.xml hello en una ubicación segura o elimínelo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="ddeb8-158">Si ha generado el par de claves RSA de hello en uno de los nodos de Linux, recuerde que las claves de hello toodelete cuando termine de utilizarlos.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="ddeb8-159">HPC Pack no establece una confianza mutua si encuentra un archivo id_rsa o id_rsa.pub existente.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddeb8-160">No se recomienda ejecutar un trabajo de Linux como un administrador de clústeres en un clúster compartido, porque un trabajo enviado por un administrador se ejecuta con la cuenta raíz de Hola Hola en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="ddeb8-161">Un trabajo enviado por un usuario sin privilegios de administrador se ejecuta bajo una cuenta de usuario local de Linux con hello mismo nombre como usuario de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="ddeb8-162">En este caso, HPC Pack establece la confianza mutua para este usuario de Linux en todos los nodos de hello asignados toohello trabajo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="ddeb8-163">Puede configurar el usuario de Linux Hola manualmente hello en nodos de Linux antes de ejecutar el trabajo de Hola o HPC Pack crea usuario Hola automáticamente cuando se envía el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="ddeb8-164">Si HPC Pack crea usuario hello, HPC Pack se elimina una vez completado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="ddeb8-165">tooreduce amenaza para la seguridad, Hola se quitan las claves al finalizar la tarea hello en nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="ddeb8-166">Configuración de un recurso compartido de archivos para nodos de Linux</span><span class="sxs-lookup"><span data-stu-id="ddeb8-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="ddeb8-167">Ahora configurar un recurso compartido de archivos SMB y montar la carpeta compartida de hello en todos los nodos tooallow Hola Linux nodos tooaccess NAMD archivos de Linux con una ruta de acceso común.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="ddeb8-168">Estos son los pasos toomount una carpeta compartida en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="ddeb8-169">Se recomienda un recurso compartido de distribuciones como CentOS 6.6 que actualmente no son compatibles con los servicios de archivos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="ddeb8-170">Si los nodos de Linux compatibles con un recurso compartido de archivos de Azure, consulte [cómo toouse almacenamiento de archivos de Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="ddeb8-171">Para consultas las opciones de uso compartido de archivos con HPC Pack, consulte [Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="ddeb8-172">Cree una carpeta en el nodo principal de Hola y compártala tooEveryone estableciendo privilegios de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="ddeb8-173">En este ejemplo, \\ \\CentOS66HN\Namd es el nombre de Hola de carpeta de hello, donde CentOS66HN es el nombre de host de hello del nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="ddeb8-174">Cree una subcarpeta denominada namd2 en la carpeta compartida de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="ddeb8-175">En namd2, cree otra subcarpeta denominada namdsample.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="ddeb8-176">Extraiga los archivos NAMD de Hola de carpeta de hello mediante una versión de Windows de **tar** u otra utilidad de Windows que funciona en los archivos .tar.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="ddeb8-177">Extraer el archivo tar de hello NAMD demasiado\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="ddeb8-178">Extraer archivos del tutorial Hola en \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="ddeb8-179">Abra una ventana de Windows PowerShell y ejecute hello siga los comandos toomount Hola carpeta compartida hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="ddeb8-180">Hola primer comando crea una carpeta denominada /namd2 en todos los nodos de grupo de LinuxNodes Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ddeb8-181">segundo comando de Hello monta Hola compartido carpeta //CentOS66HN/Namd/namd2 en la carpeta de hello con dir_mode y file_mode too777 de conjunto de bits.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="ddeb8-182">Hola *nombre de usuario* y *contraseña* Hola comando debe ser credenciales de Hola de un usuario en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="ddeb8-183">Hola "\\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ddeb8-184">"\\`,"significa Hola"," (coma) forma parte del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="ddeb8-185">Crear un toorun de secuencia de comandos de Bash un trabajo NAMD</span><span class="sxs-lookup"><span data-stu-id="ddeb8-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="ddeb8-186">El trabajo NAMD necesita un *nodelist* de archivos para **charmrun** toodetermine número de Hola de nodos toouse al iniciar NAMD procesos.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="ddeb8-187">Usar una secuencia de comandos de Bash que genera el archivo de lista de nodos de hello y se ejecuta **charmrun** con este archivo de lista de nodos.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="ddeb8-188">Después puede enviar un trabajo NAMD al administrador del clúster de HPC que llama a este script.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="ddeb8-189">Con un editor de texto de su elección, cree una secuencia de comandos de Bash en carpeta de /namd2 de Hola que contiene los archivos de programa Hola NAMD y asígnele el nombre hpccharmrun.sh. Para una rápida de prueba de concepto, copie el script de hpccharmrun.sh de ejemplo de Hola Hola final de este artículo y vaya demasiado[enviar un trabajo NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="ddeb8-190">Guarde el script como un archivo de texto con terminaciones de línea de Linux (solo LF, no CR LF).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="ddeb8-191">Esto garantiza que se ejecuta correctamente hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="ddeb8-192">A continuación, encontrará información sobre lo que hace este script de Bash.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="ddeb8-193">Defina algunas variables.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="ddeb8-194">Obtener información sobre el nodo de variables de entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="ddeb8-195">$NODESCORES almacena una lista de palabras divididas de CCP_NODES_CORES $.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="ddeb8-196">$COUNT es el tamaño de Hola de $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="ddeb8-197">formato de Hello para la variable de hello $CCP_NODES_CORES es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="ddeb8-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="ddeb8-198">Esta variable muestra hello número total de nodos, nombres de nodo y número de núcleos en cada nodo que se asignan toohello trabajo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="ddeb8-199">Por ejemplo, si el trabajo de hello necesita 10 toorun de núcleos, valor de Hola de $CCP_NODES_CORES es similar a:</span><span class="sxs-lookup"><span data-stu-id="ddeb8-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="ddeb8-200">Si no se establece la variable de hello $CCP_NODES_CORES, inicie **charmrun** directamente.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="ddeb8-201">(Esto solo debe producirse al ejecutar este script directamente en los nodos de Linux).</span><span class="sxs-lookup"><span data-stu-id="ddeb8-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="ddeb8-202">O bien cree un archivo de lista de nodos para **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="ddeb8-203">Ejecutar **charmrun** con el archivo de lista de nodos de hello, obtener su estado de retorno y quitar el archivo de lista de nodos de Hola Hola final.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="ddeb8-204">${CCP_NUMCPUS} es otra variable de entorno establecida por el nodo principal de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="ddeb8-205">Almacena el número de hello total de núcleos asignados toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="ddeb8-206">Usamos toospecify número de Hola de procesos para charmrun.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="ddeb8-207">Salir con hello **charmrun** devolver el estado.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="ddeb8-208">A continuación encontrará información de hello en archivo de nodelist hello, qué secuencia de comandos de hello genera:</span><span class="sxs-lookup"><span data-stu-id="ddeb8-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="ddeb8-209">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ddeb8-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="ddeb8-210">Submit a NAMD job</span><span class="sxs-lookup"><span data-stu-id="ddeb8-210">Submit a NAMD job</span></span>
<span data-ttu-id="ddeb8-211">Ahora está listo toosubmit un trabajo NAMD en el Administrador de clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="ddeb8-212">Conecte tooyour nodo principal del clúster e inicie el Administrador de clústeres HPC.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="ddeb8-213">En **administración de recursos**, asegúrese de que sean nodos de proceso de Linux de Hola Hola **Online** estado.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="ddeb8-214">Si no lo están, selecciónelos y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="ddeb8-215">En **Administración de trabajos**, haga clic en **Nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="ddeb8-216">Escriba un nombre para el trabajo como *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nuevo trabajo HPC][namd_job]
5. <span data-ttu-id="ddeb8-218">En hello **detalles del trabajo** página, en **recursos de trabajo**, seleccione Hola tipo de recurso como **nodo** conjunto hello y **mínimo** too3.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="ddeb8-219">, se ejecuta el trabajo de hello en tres nodos de Linux y cada nodo tiene cuatro núcleos.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![Recursos del trabajo][job_resources]
6. <span data-ttu-id="ddeb8-221">Haga clic en **editar tareas** en Hola de navegación izquierdo y, a continuación, haga clic en **agregar** tooadd un trabajo de toohello de tarea.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="ddeb8-222">En hello **detalles de la tarea y redirección de E/S** Hola conjunto siguiente de valores de la página:</span><span class="sxs-lookup"><span data-stu-id="ddeb8-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="ddeb8-223">**Línea de comandos**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="ddeb8-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="ddeb8-224">Hello línea de comandos anterior es un comando único sin saltos de línea.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="ddeb8-225">Tooappear se ajusta en varias líneas en **línea de comandos**.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="ddeb8-226">**Directorio de trabajo** - /namd2</span><span class="sxs-lookup"><span data-stu-id="ddeb8-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="ddeb8-227">**Mínimo** - 3</span><span class="sxs-lookup"><span data-stu-id="ddeb8-227">**Minimum** - 3</span></span>
     
     ![Detalles de la tarea][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="ddeb8-229">Establecer directorio de trabajo de hello aquí porque **charmrun** intenta toonavigate toohello mismo directorio de trabajo en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="ddeb8-230">Si no se ha configurado el directorio de trabajo de hello, HPC Pack inicia comando hello en una carpeta de forma aleatoria con nombre creada en uno de los nodos de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="ddeb8-231">Esto hace que Hola siguiente error en hello otros nodos: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid este problema, especifique una ruta de acceso de carpeta que puede tener acceso a todos los nodos como directorio de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="ddeb8-232">Haga clic en **Aceptar** y, a continuación, haga clic en **enviar** toorun este trabajo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="ddeb8-233">De forma predeterminada, HPC Pack envía trabajo hello como su cuenta de usuario que ha iniciado la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="ddeb8-234">Un cuadro de diálogo le solicite tooenter Hola nombre y contraseña tras hacer clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Credenciales del trabajo][creds]
   
   <span data-ttu-id="ddeb8-236">En determinadas condiciones, HPC Pack recuerda la información de usuario de hello antes de entrada y no mostrar este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="ddeb8-237">toomake HPC Pack mostrarla de nuevo, escriba Hola siguiente comando en un símbolo del sistema y, a continuación, enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="ddeb8-238">trabajo con Hello tarda varios toofinish minutos.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="ddeb8-239">Buscar el registro de trabajo de hello en \\ <headnodeName>en los archivos de salida de hello y \Namd\namd2\namd2_hpccharmrun.log \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="ddeb8-240">Si lo desea, inicie VMD tooview los resultados del trabajo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="ddeb8-241">pasos de Hola para visualizar los archivos de salida de hello NAMD (en este caso, un moléculas de proteínas ubiquitin en una esfera de agua) son más allá del ámbito de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="ddeb8-242">Consulte el [tutorial de NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ddeb8-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Resultados del trabajo][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="ddeb8-244">Archivos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ddeb8-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="ddeb8-245">Archivo de configuración XML de ejemplo para la implementación de clústeres mediante scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddeb8-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="ddeb8-246">Archivo cred.xml de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ddeb8-246">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="ddeb8-247">Script hpccharmrun.sh de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ddeb8-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
