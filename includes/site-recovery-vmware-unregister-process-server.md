<span data-ttu-id="91c37-101">Hola pasos toounregister un servidor de proceso depende de su estado de conexión con el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="91c37-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="91c37-102">Anulación del registro de un servidor de procesos que se encuentra en estado conectado</span><span class="sxs-lookup"><span data-stu-id="91c37-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="91c37-103">Remoto en el servidor de procesos de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="91c37-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="91c37-104">Iniciar hello **el Panel de Control** y abra **programas > desinstalar un programa**</span><span class="sxs-lookup"><span data-stu-id="91c37-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="91c37-105">Desinstalar un programa por su nombre de hello **servidor de configuración o proceso de recuperación de Microsoft Azure sitio**</span><span class="sxs-lookup"><span data-stu-id="91c37-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="91c37-106">Cuando haya efectuado el paso 3, puede desinstalar las **dependencias del servidor de configuración o de procesos de Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="91c37-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="91c37-107">Anulación del registro de un servidor de procesos que se encuentra en estado desconectado</span><span class="sxs-lookup"><span data-stu-id="91c37-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="91c37-108">Hola de uso pasos indicados a continuación debe usarse si no hay ninguna máquina virtual de manera toorevive hello en qué Hola se instaló el servidor de procesos.</span><span class="sxs-lookup"><span data-stu-id="91c37-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="91c37-109">Inicie sesión en el servidor de configuración de tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="91c37-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="91c37-110">Abra un símbolo del sistema administrativo y busque el directorio de toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="91c37-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="91c37-111">Ahora ejecute el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="91c37-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="91c37-112">Esto depurarán las detalles Hola Hola del servidor de procesos del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="91c37-112">This will purge hello details of hello process server from hello system.</span></span>
