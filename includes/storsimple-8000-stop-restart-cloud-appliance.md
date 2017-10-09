#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop e inicie una aplicación en la nube

1. toostop un dispositivo en la nube, vaya toohello máquina virtual para su dispositivo en la nube.
    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. En la barra de comandos de hello, haga clic en **detener**.

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Cuando se le pida confirmación, haga clic en **Sí**.

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Cuando detiene una máquina virtual, esta se desasigna. Mientras se está deteniendo el dispositivo de nube de hello, su estado es **Deallocating**. Cuando se haya detenido el dispositivo de nube de hello, su estado es **detenido (desasignado)**.

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Una vez que se detiene una máquina virtual, haga clic en **iniciar** (botón esté disponible) toostart Hola máquina virtual. Después de dispositivo de hello en la nube se ha iniciado, su estado es **iniciado**.

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Usar hello después cmdlets toostop e iniciar una aplicación de nube.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart un dispositivo de nube

toorestart un dispositivo en la nube, vaya toohello máquina virtual para su dispositivo en la nube. En la barra de comandos de hello, haga clic en **reiniciar**. Cuando se le pida, confirme Hola reinicio. Cuando esté listo para toouse aparato de nube de hello, su estado es **ejecutando**.

![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Usar hello siguiente cmdlet toorestart un dispositivo de nube.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

