## <a name="defining-a-backup-policy"></a>Definición de una directiva de copia de seguridad
Una directiva de copia de seguridad define una matriz de cuando se toman instantáneas de datos de Hola y cuánto tiempo se conservan esas instantáneas. Al definir una directiva para la copia de seguridad de una máquina virtual, puede desencadenar un trabajo de copia de seguridad *una vez al día*. Cuando se crea una nueva directiva, es el almacén de toohello aplicado. interfaz de la directiva de copia de seguridad de Hello tiene el siguiente aspecto:

![Directiva de copia de seguridad](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate una directiva:

1. Escriba un nombre para hello **nombre de la directiva**.
2. Puede tomar instantáneas de los datos con un intervalo diario o semanal. Hola de uso **frecuencia de copia de seguridad** toochoose del menú desplegable si se toman instantáneas de datos diario o semanal.
   
   * Si elige un intervalo diario, use Hola resaltado control tooselect Hola hora Hola para instantáneas de Hola. hora de hello toochange, anule la selección de hora de Hola y seleccione Hola hora nueva.
     
     ![Directiva de copia de seguridad diaria](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Si elige un intervalo de periodicidad semanal, utilice Hola controles resaltado tooselect Hola día (s) de la semana de hello y la hora de Hola de instantánea de día tootake Hola. En el menú de día de hello, seleccione uno o varios días. En el menú de la hora de hello, seleccione una hora. hora de hello toochange, anular la selección de hora seleccionada hello y seleccione Hola hora nueva.
     
     ![Directiva de copia de seguridad semanal](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. De forma predeterminada, todas las opciones de **Duración de retención** están seleccionadas. Desactive cualquier límite de intervalo de retención no desea toouse. A continuación, especifique hello interval(s) toouse.
   
    Mensual y anual duraciones de retención le permiten instantáneas de hello toospecify tomando como base un incremento semanal o diario.
   
   > [!NOTE]
   > Al proteger una máquina virtual, un trabajo de copia de seguridad se ejecuta una vez al día. hora de Hello cuando se ejecuta copia de seguridad de hello es Hola igual para cada intervalo de retención.
   > 
   > 
4. Después de establecer todas las opciones de directiva de hello, en parte superior de Hola de hoja de hello, haga clic en **guardar**.
   
    nueva directiva de Hello es el almacén de toohello aplica inmediatamente.

