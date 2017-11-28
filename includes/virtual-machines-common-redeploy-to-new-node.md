## <a name="use-the-azure-portal"></a><span data-ttu-id="1a8d5-101">Uso del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1a8d5-101">Use the Azure portal</span></span>
1. <span data-ttu-id="1a8d5-102">Seleccione la máquina virtual que quiera volver a implementar y el botón *Volver a implementar* en la hoja *Configuración*.</span><span class="sxs-lookup"><span data-stu-id="1a8d5-102">Select the VM you wish to redeploy, then select the *Redeploy* button in the *Settings* blade.</span></span> <span data-ttu-id="1a8d5-103">Es posible que deba bajar para ver la sección **Soporte y solución de problemas** que contiene el botón Volver a implementar, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a8d5-103">You may need to scroll down to see the **Support and Troubleshooting** section that contains the 'Redeploy' button as in the following example:</span></span>
   
    ![Hoja Máquina virtual de Azure](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. <span data-ttu-id="1a8d5-105">Para confirmar la operación, haga clic en el botón *Volver a implementar*:</span><span class="sxs-lookup"><span data-stu-id="1a8d5-105">To confirm the operation, select the *Redeploy* button:</span></span>
   
    ![Hoja Volver a implementar una máquina virtual](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. <span data-ttu-id="1a8d5-107">El valor de **Estado** de la máquina virtual cambia a *Actualizando*, puesto que la máquina virtual se prepara para implementarse de nuevo, como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1a8d5-107">The **Status** of the VM changes to *Updating* as the VM prepares to redeploy, as shown in the following example:</span></span>
   
    ![Máquina virtual actualizando](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. <span data-ttu-id="1a8d5-109">El valor de **Estado** pasa luego a *Iniciando* cuando la máquina virtual se inicia en un nuevo host de Azure, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a8d5-109">The **Status** then changes to *Starting* as the VM boots up on a new Azure host, as shown in the following example:</span></span>
   
    ![Máquina virtual iniciando](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. <span data-ttu-id="1a8d5-111">Cuando la máquina virtual finaliza el proceso de arranque, el **estado** vuelve a *En ejecución*, lo que indica que la máquina virtual se ha vuelto a implementar correctamente:</span><span class="sxs-lookup"><span data-stu-id="1a8d5-111">After the VM finishes the boot process, the **Status** then returns to *Running*, indicating the VM has been successfully redeployed:</span></span>
   
    ![Máquina virtual en ejecución](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)

