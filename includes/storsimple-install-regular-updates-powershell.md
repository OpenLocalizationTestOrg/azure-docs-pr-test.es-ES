<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="090df-101">tooinstall actualizaciones periódicas a través de Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="090df-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="090df-102">Abra la consola serie del dispositivo de Hola y seleccione la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="090df-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="090df-103">Escriba la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="090df-103">Type hello password.</span></span> <span data-ttu-id="090df-104">es la contraseña predeterminada de Hello *Password1*.</span><span class="sxs-lookup"><span data-stu-id="090df-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="090df-105">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="090df-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="090df-106">Se le notificará si hay actualizaciones disponibles y si las actualizaciones de hello son perjudiciales o no perjudiciales.</span><span class="sxs-lookup"><span data-stu-id="090df-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="090df-107">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="090df-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="090df-108">se iniciará el proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="090df-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="090df-109">Este comando aplica sólo tooregular actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="090df-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="090df-110">Este comando se ejecuta en un solo controlador, pero se actualizarán ambos controladores.</span><span class="sxs-lookup"><span data-stu-id="090df-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="090df-111">Puede que observe una conmutación por error del controlador durante el proceso de actualización de hello; Sin embargo, Hola conmutación por error no afectará a la disponibilidad del sistema o la operación.</span><span class="sxs-lookup"><span data-stu-id="090df-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

