# Bioinformatic-Protocols-for-NLHPC
Documentación con Tips y Buenas Practicas para el uso del NLHPC para tareas de Bioinformática y/o similares<br>

## 1. Creación de cuentas, solicitudes de horas de computo, CPUs y Storage.
### 1.1 Creación de cuentas

La creación de cuentas del NLHPC se puede separar en 2 grupos. 1) Usuarios nuevos sin conexion al NLHPC y 2) Usuarios que seran parte de un grupo ya existente en el NLHPC.

* En el primer grupo de usuarios, la creación de cuentas se da de forma exclusiva a un/una PI o investigadores jovenes, los cuales deberan rellenar el siguiente formulario con la información correspondiente https://solicitudes.nlhpc.cl/.

* En el caso de que el PI este generando una cuenta para su grupo o equipoy que requiera mas de 1 cuenta, lo ideal es generar 1 cuenta de PI en https://solicitudes.nlhpc.cl/ y cuentas individuales para cada miembro del grupo, es decir.
```
   a) 1 Cuenta de PI.
   b) N Cuentas, 1 por cada miembro del Team.
 ```  
La recomendación principal de la creación de cuentas para un grupo es idealmente, asignar un Nombre del Team Investigación. Como ejemplo: CRG-LAB1, CRG_UOH o, en mi caso particular, Mathomics.
Esto facilitara luego, la creación de cuentas para miembros del mismo grupo, y la asignación de permisos, protocolos y tools que el grupo completo necesitara eventualmente.

La recomendación principal es que cada nueva cuenta sea creada o solicitada por 1 solo miembro de cada Team o Grupo. Esta tarea puede recaer directamente al PI o puede ser un encargado seleccionado.

Para mantener el orden y la trazabilidad de los datos, lo ideal es que cada usuario pueda acceder a 1 sola cuenta. Compartir claves incurre una alta probabilidad de accesos no autorizados, uso de recursos no controlados o eliminación de datos sin consentimiento.
En el caso de necesitar una cuenta de datos la cual sera utilizada solo por periodos cortos de tiempo, con varios usuarios distintos, se recomienda crear una cuenta especial de invitado. Esta cuenta debe estar registrada con el mismo PI y bajo el mismo Team.
Por lo general estas cuentas se usan solo para compartir datos con otros investigadores, o estudiantes en practica, los cuales no necesitan cuentas permanentes individuales.<br>

### 1.2 Solicitudes de horas de computo, CPUs y storage.

Durante la creación de cuentas de cuentas del PI, se requerira establecer una cuota de horas de computo. Esta solicitud se asignara como limite de ejecución de tareas con una duración de 1 año, a partir de la fecha de la primera solicitud. Estas horas de computo se estableceran como limite para cada Team, por lo que no es necesario generar una peticion de horas de computo por cada cuenta. 

En el caso que las horas de computo se cumplan, ninguna cuenta del Team podra seguir ejecutando tareas, hasta generar una nueva solicitud en https://solicitudes.nlhpc.cl/.
Por lo general, una solicitud de horas de computo debera tomar en cuenta la cantidad de miembros, las tareas que se necesitan ejecutar, la cantidad de veces que se necesita ejecutar la misma tarea. 
Como un buen estimador en bioinformática, la cantidad de horas para limpiar, ensamblar, anotar y analizar genomas durante 1 año calendario es de entre 20.000 y 50.000 horas por cuenta.

En el caso de cuentas con gran volumen de datos y varos analisis al año, las horas por cuenta pueden superar facilmente los 250.000 horas de computo.
La recomendación es: Para Teams nuevos: entre 10.000 a 15.000 horas de computo por cuenta. Para Teams con experiencia, entre 50.000 a 70.000 horas de computo por cuenta.

En el caso de que la cantidad de horas de computo solicitadas sea muy por debajo de lo necesario por cada Team, el equipo de Soporte del NLHPC enviara un correo a cada cuenta con la notificación de que el numero de horas esta por acabarse o completamente utilizada. En esta notificación, cada cuenta tendra desglozado el numero de horas que se utilizaron. 

Para no repetir una nueva solicitud de horas de computo cada 4 o 6 meses, lo ideal es utilizar la información obtenida en la notificación del NLHPC y reajustar la petición para que coincida con el periodo de 12 meses.

#### El cobro de horas de computo se realiza sobre el uso real, y no sobre las horas solicitadas en la creación de cuentas. ####<br>
### 1.3 CPUs y Storage

Al crear una nueva cuenta en el NLHPC, si no se especifican la cantidad de recursos de CPU y Storage, cada cuenta tendra por default 88 CPU y 120Gb de Storage. En el caso de las CPUs significa que el usuario, puede utilizar como máximo 88 CPUs al mismo tiempo durante procesos de ejecución, es decir, si ejecutamos 3 procesos con 40 CPU cada 1.

      a) Proceso 1 con 40 CPU. Este proceso se ejecutara sin problemas, siempre y cuando existan recursos en el NLHPC. 
      b) Proceso 2 con 40 CPU. Este proceso se ejecutara sin problemas, siempre y cuando existan recursos en el NLHPC.
      c) Proceso 3 con 40 CPU. Este proceso no se podra ejecutar hasta que el proceso a) o b) terminen. 

En el caso del Storage, este valor es el limite maximo con el cual podremos guardar nuestros archivos o tareas. Si se da la instancia de que nuestra cuota de Storage esta en su limite, no se podran seguir ejecutando tareas, aun teniendo CPUs y horas de computo disponible. 
En el caso de que lleguemos al limite del Storage, durante la ejecución de una de nuestras tareas, esta terminara antes forzosamente, y se notificara al usuario de la falta de espacio en nuestra cuenta.

#### Tanto la cantidad de CPUs como el Storage se pueden solicitar de forma indivual para para cuenta/usuario, por lo que es necesario revisar los requerimientos de cada uno ####

A modo general el uso de recursos optimo es alrededor de:

> 100 CPUs y 500Gb para Team nuevos. <br>
> 200+ CPUs y 1Tb+ de Storage para Teams antiguos <br>

<br>
<br>

## 2. Login al NLHPC.
<br>
Una vez creada nuestra cuenta, podemos acceder al Login del NLHPC. El proceso actual, con fecha 2025 es tal como:

```
ssh -p 4603 mi_cuenta@leftraru.nlhpc.cl
```

Con este comando podremos entrar al NLHPC en cualquier parte del pais, sin necesidad de una VPN.
En el caso de encontrarnos temporalmente en el extranjero, se debera utilizar una VPN para anclarnos primero a Chile, y luego acceder al servidor de manera normal.

<br>
<br>

## 3. Instalación de software mediante gestor de paquetes, Modo SUDO y Module LOAD.<br>

### 3.1 Instalación de software mediante gestor de paquetes
La mayoria de las tools y paquetes en Bioinformática se pueden encontrar en gestores de paquetes altamente utilizados en ciencia, tales como:

```
Anaconda3
Miniconda
Mamba
HomeBrew
PERL
PIP
```
Tanto Anaconda3 como Miniconda funcionan sin problemas en el NLHPC (https://www.anaconda.com/docs/getting-started/miniconda/install#linux-x86) y se pueden instalar de manera local en nuestra cuenta como:

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash ~/Miniconda3-latest-Linux-x86_64.sh
source ~/.bashrc
```
Una vez instalados, es tan simple como instalar cualquier tools que exista en el gestor de paquetes, en nuestro caso, usaremos como ejemplo Meme Suite. (https://anaconda.org/bioconda/meme):

```
conda install bioconda::meme
conda install bioconda/label/cf201901::meme
```

Eventualemte, la instalación se ejecutara sin problemas y podremos utilizar la herrameinta como corresponda.<br>

### 3.2 Modo SUDO

En el caso de nuestros computadores personales, podremos acceder a la instalación de tareas mediante SUDO o super usuario.
Este metodo de instalación esta restringido para todas las cuentas del NLHPC a exepcion del equipo de soporte, por lo que ninguna herramienta se podra instalar mediante este metodo, es decir, los comandos tales como:

```
sudo install tool
sudo apt install tool
```
NO son validos.<br>
En el caso de necesitar instalar una tool que requiera especificamente este comando, existen 2 soluciones especificas.<br>

#### A. Instalación local con el codigo fuente. ####

Para la instalación local de nuestra tool, primero necesitaremos el codigo fuente de la herramienta. Por lo general cualquier tool que utilice el comando SUDO, tiene un codigo fuente, el cual se puede descargar desde la pagina web del software o desde github. En nuestro caso, seguiremos el ejemplo de MEME Suite (https://web.mit.edu/meme/current/share/doc/install.html).

```
tar zxf meme_4.11.4.tar.gz
cd meme_4.11.4
./configure --prefix=$HOME/meme --with-url=http://meme-suite.org --enable-build-libxml2 --enable-build-libxslt
make
make test
make instal
```

En el ejemplo anterior, podemos instalar localmente nuestra tool utilizando el comando especifico:
```
--prefix=$HOME/my_carpeta_personal
o
--prefix=/home/my_cuenta/my_carpeta_personal
```

En el caso de que no exista la opción de instalación del codigo fuente, o encontremos errores dentro del proceso, podemos utilizar la opcion B.<br>

#### B. Solicitud de instalación al equipo de Soporte NLHPC ####

Cada vez que necesitemos instalar herramientas que parecen demasiado complicadas o requieren librerias que no podemos encontrar. Lo mejor es realizar una solicitud al equipo de Soporte del NLHPC (soporte@nlhpc.cl) mediante un correo.

```
at@ soporte@nlhpc.cl
Asunto: Instalacion tool Meme Suite:
_______________________________________

Correo.....

```
En nuestro correo de solicitud debemos agregar:

> El link de la tool a instalar. <br>
> El o los usuarios a los que se desea instalar la tool.

En el caso de que nuestra tool sea requerida por todo nuestro Team, existe la posibilidad de implementar la herramienta como Modulo, y que quede en el registro de tools instaladas del NLHPC para que pueda ser cargada por cualquier usuario, inclusive fuera de nuestro Team.<br>
### 3.3 Module Load 

El NLHPC tiene pre-instaladas una variedad de tools las cuales han sido testeadas y deberian ejecutarse sin problemas en cualquier cuenta del servidor.

Para acceder al catalogo de herramientas pre-instaladas, podemos presionar en la consola:

```
$ module load [TAB]
Display all 1113 possibilities? (y or n)
amber                                         MCTDH
Amber                                         MCTDH/86.3
amber/20-mpi-zen4-w                           mercurial
Amber/22-fosscuda                             mercurial/6.7.3-zen4-g
Amber/22.intel-2019b                          merra2wps
Amber/24-foss-2023b                           merra2wps/08-2021
amber/24-rocm-gcc-14.2.0-zen4                 MESH
amdblis                                       MESH/1.4
........
........
........

```

Este comando listara todas las tools existentes, en el caso de buscar una nombre especifico, podemos poner las inciales o el nombre completo.

```
$ module load M[TAB]
M4                                       MCR/R2018a                               Mono
M4/1.4.17                                MCR/R2020b                               Mono/6.12.0.122
M4/1.4.18                                MCTDH                                    Mothur/intel2022.00
M4/1.4.19                                MCTDH/86.3                               Mothur/intel2022.00/1.48.1
Magics                                   MEGAHIT                                  MPC
Magics/4.13.0                            MEGAHIT/1.2.9                            MPC/1.0.1
Mako                                     Mesa                                     MPC/1.2.1
Mako/1.1.4                               Mesa/21.1.7                              MPFR
MALT                                     MESH                                     MPFR/2.4.2
MALT/0.5.2                               MESH/1.4                                 MPFR/3.1.2
Mathematica                              MESH/1.4.2-symbols                       MPFR/4.1.0
Mathematica/13.3                         Meson                                    MPPCrystal17
MathGL                                   Meson/0.58.2                             MPPCrystal17/1.0.2
MathGL/8.0.1                             MetaBAT                                  MuJoCo
MathWorksServiceHost                     MetaBAT/2.15                             MuJoCo/2.1.1
MathWorksServiceHost/2024.13.0.2         METIS                                    MultiNest
Matlab                                   METIS/5.1.0                              MultiNest/3.10
MATLAB                                   Miniconda2                               MultiQC
Matlab/2017                              Miniconda2/4.7.10                        MultiQC/1.14
MATLAB/2019b                             Miniconda3                               MUMmer
Matlab-Runtime                           Miniconda3/4.5.12                        MUMmer/4.0.0beta2
Matlab-Runtime/amd                       Miniconda3/4.9.2                         MUMmer/4.0.0rc1
Matlab-Runtime/intel                     MinPath                                  MUMPS
Maven                                    MinPath/1.6                              MUMPS/5.4.0-metis
Maven/3.6.3                              Molekel                                  MUMPS/5.5.1-metis
MCR                                      Molekel/5.4.0-Linux_x86_64               MUMPS/5.7.3-metis
MCR/R2016b                               Molpro
MCR/R2017a                               Molpro/mpp-2020.2.1.linux_x86_64_openmp
```

El comando module load o ml para abreviar, es sencible a mayusculas y minisculas:
```
$ module load M[TAB]
$ module load m[TAB]
$ module load ME[TAB]
$ module load Me[TAB]
$ module load me[TAB]
```

Cada uno de los comandos anteriores generara resultados diferentes, por lo que es necesario tomar precauciones a la hora de cargar un modulo.

Ademas, existen diferentes versiones para las tools pre-instaladas, por lo que habra que poner atención a la hora de cargar la tool y version correctas.

```
$ module load Java
Java                        Java/17.0.2                 Java/1.8.0_202
Java/11                     Java/17.0.4                 Java/1.8.0_232-b09-OpenJDK
Java/11.0.2                 Java/1.8                    Java/23.0.2
```
<br>
<br>

## 4. Ejecución de tareas / Jobs en la cola de procesos y solicitud de recursos .<br>

### 4.1 Archivo de ejecución de tareas / Jobs <br>

Todas las tareas que necesitemos ejecutar en el NLHPC deben entrar en la cola de procesos a travez de un archivo de ejecución.
Ejecutar tareas directamente en en consola, sin pasar por la cola de procesos, tiene un tiempo limite maximo de ejecucion de 30 minutos.
Lo ideal es siempre utilizar la cola de procesos, puesto que correr directamente desde la consola utiliza los recuros del sistema de login, el cual relentiza toda la navegación en el sitema NLHPC.

Tareas pequeñas como parsear archivos, uso de "grep" o "awk" se pueden realizar perfectamente en la consola de login. Tareas como ensambles, anotaciones, u otros que requieran mas de un CPU o bastante memoria RAM estan prohibidos.

En el caso que requiramos ejecutar una tarea en la cola de procesos, para ello necesitaremos un archivo de ejecución. A continuacion tendremos uno basico que nos servira para la mayoria de nuestras tareas.

1) Primero, debemos crear un archivo con un editor de texto, para ello usaremos VIM.

```
$ vim standar_job.sh
```

2) Luego dentro del archivo podremos escribir la siguiente configuración:
   
```
#SBATCH -J [JOB_NAME]
#SBATCH -p [PARTITION]
#SBATCH -n [NUMBER OF NODES]
#SBATCH -c [NUMBER OF CPU]
#SBATCH --mem=[RAM MEMORY IN GB]
#SBATCH -o [ERROR FILE] 
#SBATCH -e [OUTPUT FILE]
#SBATCH -t [EXECUTION TIME]
#SBATCH --mail-user=your-email-here@examp.com
#SBATCH --mail-type=ALL 
```
<br>

### Revisemos ahora cada uno de los parametros: ####

<br>


```
#SBATCH -J [JOB_NAME] :             Aca ira el nombre de nuestra tarea. Utilizar nombres cortos y faciles de identificar
                                    es lo recomendado
```


```
#SBATCH -p [PARTITION] :            En este campo ira la particion del NLHPC al cual enviaremos nuestra tarea.
                                    Actualmente existen 6 particiones que los usuarios pueden utilzar.
                                    Las caracteristicas de cada particion se encuentran en https://dashboard.nlhpc.cl/
                                    estas particiones son:
                                    main
                                    general
                                    largemem
                                    mi210
                                    mi100
                                    v100<br>
                                    Se debera escoger la partición segun las necesidades que tengamos para ejecutar nuestras
                                    tools.
                                    La mayor parte de nuestras tareas correran en "general", "main" o "largemem", puesto que
                                    CPU y RAM componen ma mayor parte de las tools en Bioinformatica.

```


```
#SBATCH -n [NUMBER OF NODES]:       Este parametro indica el numero de NODOS para ejecutar nuestras tareas. En Bioinformatica
                                    muy pocas tools estan optimizadas para ejecutarse en mas de 1 NODO, por lo que es
                                    practicamente improbable utilizar mas de 1.
```



```
#SBATCH -c [NUMBER OF CPU] :        Aca se establece el numero de CPUs a utilizar. Por mas que podamos pedir 100 CPUs,
                                    la mayor parte de las tools en Bioinformatica solo escalan hasta 12 o 20 CPUS, con algunas
                                    exepciones llegando a los 40 CPU.
                                    Pedir mas no nos dara una ventaja real de tiempo de ejucion. Al contrario, perderemos
                                    mas tiempo esperando que se liberen los recursos que ejuctar las tareas con la mitad
                                    de CPUs.
                                    - El formato de esta variable es: Numeros enteros del 1 al 256, dependiendo de cada
                                    partición:
                                    Limite CPU particion main      = 256
                                    Limite CPU particion general   =  44
                                    Limite CPU particion largemem  =  44
```


```
#SBATCH --mem= [RAM MEMORY IN GB] : Este parametro reserva la cantidad de memoria RAM que necesitara nuestra tool.
                                    La cantidad de RAM se debe establecer en relación al NODO que se esta reservando,
                                    es decir, no es posible reservar 200GB de RAM en la partición "general" ni 1TB de RAM
                                    en la particion "largemem".
                                    El equipo del NLHPC recomienda utilizar a lo maximo 5GB de RAM por CPU, aunque esta
                                    recomendación es casi inutilizable en Bioinformatica. En nuestro caso, existiran tools
                                    que utilizaran 200 a 400Gb de RAM, pero se ejecutaran solo en 20 a 40 CPU.
                                    Mas adelante veremos algunos ejemplos de ejecución.
                                    - El formato de esta variable es: Numeros enteros del 1 al 256, seguido del sufijo GB,
                                    dependiendo de cada partición:
                                    Limite RAM particion main      = 710GB
                                    Limite RAM particion general   = 175GB
                                    Limite RAM particion largemem  = 710GB

   
```

```
#SBATCH -o [ERROR FILE] :           Este archivo contendra la salida de errores de la ejecucion de nuestra tool.
                                    Aca podremos revisar si nuestra ejecución fue exitosa o si existio algun problema
                                    particular que produjo la terminacion forsoza de nuestro job.
                                    Es importante siempre configurar este archivo, pues es la unica forma real de
                                    reconocer errores para futuras ejecuciones
```

```
#SBATCH -e [OUTPUT FILE] :          Este archivo contiene la salida por consola de nuestra tool. Cuando la
                                    herramienta que estamos tratando de ejecutar no tiene configurado un
                                    archivo de output, la salida de nuestro programa sera escrita aqui. La mayor
                                    parte de los archivos output sera un mensage propio de cada tool con informacion
                                    y tiempo de ejecucion.
```

```
#SBATCH -t [EXECUTION TIME] :      Este parametro a sido recientemente introducido en el año 2025 y reserva el tiempo de
                                   ejecucion de nuestra tarea. No es necesario ser extremadamente exacto en los tiempos de
                                   ejecucion, pero generalmente podemos utilizar horas o dias sin mayores cambios de esta
                                   variable.
                                   Si nuestra tarea supera el tiempo reservado, esta se cancelara automaticamente, y
                                   tendremos que volver a lanzarla desde el inicio.
                                   - El formato de esta variable es: dd-hh:mm:ss
                                   - Un ejemplo para 1 dia, 3 horas y 20 minutos de ejecución seria: 1-03:20:00
```
```
#SBATCH --mail-user=your-email-here@examp.com : Estas Variables son opcionales y generaran un correo automatico con  
#SBATCH --mail-type=ALL                         información de nuestra tarea, este se encuentre en "ESPERA", "EJECUCION".
                                                "TAREA CANCELADA", "TAREA TERMINADA", entre otros.
```

<br>

### 4.2 Solicitud de Recursos ###

Una vez revisado cada campo de nuestro Archivo de ejecución de tareas, podremos ahora solicitar la cantidad de recusos y el tiempo que estimemos conveniente.
Como se menciono brevemente, una tool que pueda utilizar mas de 1 CPU, no necesariamente se ejecutara 70 veces mas rapico al pedir 70 CPUs.

La experiencia nos dice que la mayor cantidad de herramientas grandes escala solo hasta los 20 a 40 CPU. Ademas, es mucho mas eficiente dividir nuestras tareas
en fragmentos o chunks y ejecutarlos al mismo tiempo, que ejecutar todo junto pidiendo mas CPU, es decir, ejecutar la misma tarea, dividida en 5 partes con 20 CPU cada una, sera mucho mas eficiente que ejecutar la misma tarea completa 1 vez con 100 CPU.

De todas formas, existe un catalogo infino te tools que podremos utilizar, y aunque no podemos conocer a priori sus requerimientos de ejecucion de maxima eficiencia, la experiencia nos brindara un mejor juico a la hora de escoger recursos.
<br>
Pero a falta de tiempo, he aqui algunos ejemplos.

### TAREAS DE ASSEMBLY. 1 Metegenoma grande de 200+ Millones de Reads. Tool: MEGAHIT ###

```
#SBATCH -p main o largemem
#SBATCH -n 1
#SBATCH -c [12-20]
#SBATCH --mem=[200GB-400GB]
#SBATCH -t 2-00:00:00
```

### TAREAS DE ANOTACION.  Mismo metagenoma, contra una base de datos de 50GB. Tool: EggNOGMapper ###

```
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [8 a 12]
#SBATCH --mem=80GB
#SBATCH -t 4-00:00:00
```

### CLUSTERING DE GENES.  400+ Millones de CDS. Tool: MMseqs2 ###

```
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [12 a 20]
#SBATCH --mem=[400GB - 500GB]
#SBATCH -t 3-00:00:00
```

### CREACION DE MAGS / BINNING. Tool: SemiBin2 ### 

```
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [12 a 20]
#SBATCH --mem=[20GB - 150GB]
#SBATCH -t [2-00:00:00 a 7-00:00:00]
```

### ANOTACION DE MAGS. 1 MAG. Tool: Bakta: ###

```
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c 2
#SBATCH --mem=20GB
#SBATCH -t 08:00:00
```

### ANOTACION DE MAGS. 1000+ MAG. Tool: DRAM: ###

```
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [12 a 20]
#SBATCH --mem=200GB
#SBATCH -t 14-23:00:00
```

Estos son algunos ejemplos de las tareas con mayor cantidad de recursos que he tenido experiencia de probar en el NLHPC. Cabe considerar que estos datos tienen un peso aproximado de TB, por lo que proyecto relativamente livianos requeriran menos recursos.
Cabe destacar que la regla de 1 CPU por cada 5GB de RAM no aplica para ninguno de los programas listados. Esta regla es mas bien una recomendación de eficiendia en programas altamente revisados, y lamentablemente, no aplica para la mayoria de herramientas bioinformáticas.
Mientras utilizemos rangos de CPU y RAM que no se salgan de extremos, como por ejemplo, ejecutar una tool single thread con 50 CPU y 700GB de RAM, no deberiamos tener mayores problemas.

#### Como recordatorio, todas las tareas / jobs, tienen un maximo tiempo de ejecucion de 30 DIAS. Luego de esto, sin importar el tiempo pedido, la tarea sera cancelada automaticamente ####


