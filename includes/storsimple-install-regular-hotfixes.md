<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="cd34f-101">tooinstall revisiones normales mediante Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="cd34f-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="cd34f-102">Conecte la consola serie del dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="cd34f-102">Connect toohello device serial console.</span></span> <span data-ttu-id="cd34f-103">Para obtener más información, consulte [paso 1: conectar la consola serie toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="cd34f-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="cd34f-104">En el menú de consola serie de hello, seleccione la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="cd34f-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="cd34f-105">Escriba la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd34f-105">Type hello password.</span></span> <span data-ttu-id="cd34f-106">es la contraseña predeterminada de Hello **Password1**.</span><span class="sxs-lookup"><span data-stu-id="cd34f-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="cd34f-107">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="cd34f-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="cd34f-108">Este comando aplica solo tooregular las revisiones.</span><span class="sxs-lookup"><span data-stu-id="cd34f-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="cd34f-109">Este comando se ejecuta en un solo controlador, pero se actualizarán ambos controladores.</span><span class="sxs-lookup"><span data-stu-id="cd34f-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="cd34f-110">Puede que observe una conmutación por error del controlador durante el proceso de actualización de hello; Sin embargo, Hola conmutación por error no afectará a la disponibilidad del sistema o la operación.</span><span class="sxs-lookup"><span data-stu-id="cd34f-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="cd34f-111">Cuando se le solicite, proporcione Hola ruta de acceso toohello carpeta compartida de red que contiene los archivos de revisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd34f-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="cd34f-112">Se le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="cd34f-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="cd34f-113">Tipo de **Y** tooproceed con la instalación de revisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd34f-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

