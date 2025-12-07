# Bioinformatic-Protocols-for-NLHPC
#### Documentación con Tips y Buenas Practicas para el uso del NLHPC para tareas de Bioinformática y/o similares<br>

El servicio del Laboratorio Nacional de Computación de Alto Rendimiento o [NLHPC](url:https://www.nlhpc.cl/) es un supercomputador a gran escala diseñado para dar respuesta a los desafíos cientificos y tecnológicos de nuestro pais.
Esta infraestructura está al servicio de la comunidad y puede ser utilizada en áreas como Astronomía, Ingeniería, Salud y Bioinformática, siendo esta última la que exploraremos en el siguiente documento.

Durante el transcurso de su servicio, a podido ayudar al desarrollo de la ciencia de datos del genoma humano, dar sequimiento a enfermedades como el coronavirus, y acelerado descrubrimientos importantes tanto en desiertos, oceanos y medio ambiente.
Ejemplos notables de este apoyo a la ciencia se pueden observar en publicaciones tales como:

[Genomes of the Orestias pupfish from the Andean Altiplano shed light on their evolutionary history and phylogenetic relationships within Cyprinodontiformes](https://doi.org/10.1186/s12864-024-10416-w)
[From sewage to genomes: Expanding our understanding of the urban and semi-urban wastewater RNA virome](https://doi.org/10.1016/j.envres.2025.121509)
[Fine Mapping Using Whole-Genome Sequencing Confirms Anti-Müllerian Hormone as a Major Gene for Sex Determination in Farmed Nile Tilapia (Oreochromis niloticus L.)](https://doi.org/10.1534/g3.119.400297)
[Insights into neutralizing antibody responses in individuals exposed to SARS-CoV-2 in Chile](https://doi.org/10.1126/sciadv.abe6855)
[Nutrient Scarcity in a New Defined Medium Reveals Metabolic Resistance to Antibiotics in the Fish Pathogen Piscirickettsia salmonis](https://doi.org/10.3389/fmicb.2021.734239))

No obstante, el acceso y uso del NLHPC se puede percibir como una barrera inpenetrable para nuevos usuarios, los cuales tienen que batallar no solo con el entorno UNIX, sino también, con el uso específico de estas tecnologías que distan mucho del manejo diario de nuestros computadores personales.

Para poder enfrentar este desafío, se ha preparado esta guía para orientar tanto a nuevos investigadores como usuarios antiguos, la cual permitira utilizar de manera sencilla y eficiente las instalaciones del NLHPC.



## Tabla de Contenidos
* [1. Creación de cuentas, solicitudes de horas de computo, CPUs y Storage.](#1-Creación-de-cuentas-solicitudes-de-horas-de-computo-CPU-y-Storage.)
    * [1.1 Creación de cuentas](1.1-Creación-de-cuentas)
    * [1.2 Solicitudes de horas de computo.](1.2-Solicitudes-de-horas-de-computo.)
    * [1.3 CPUs y Storage](1.3-CPUs-y-Storage)
* [2. Login al NLHPC.](2.-Login-al-NLHPC.)
* [3. Instalación de software mediante gestor de paquetes, Modo SUDO y Module LOAD](3.-Instalación-de-software-mediante-gestor-de-paquetes,-Modo-SUDO-y-Module-LOAD)
    * [3.1 Instalación de software mediante gestor de paquetes](3.1-Instalación-de-software-mediante-gestor-de-paquetes)
    * [3.2 Modo SUDO](3.2-Modo-SUDO)
    * [3.3 Module Load](3.3-Module-Load)
* [4. Archivo de ejecución de tareas / Jobs en la cola de procesos y solicitud de recursos](4.-Archivo-de-ejecución-de-tareas-/-Jobs-en-la-cola-de-procesos-y-solicitud-de-recursos)
    * [4.1 Archivo de ejecución de tareas / Jobs](4.1-Archivo-de-ejecución-de-tareas-/-Jobs)
    * [4.2 Solicitud de Recursos](4.2-Solicitud-de-Recursos)
* [5. Ejecución de tareas / jobs, Monitoreo de tareas y Cancelación de tareas](5.-Ejecución-de-tareas-/-jobs,-Monitoreo-de-tareas-y-Cancelación-de-tareas)
    * [5.1 Ejecución de tareas](5.1-Ejecución-de-tareas)
        * [5.1.1 Ejecución lineal](5.1.1-Ejecución-lineal)
        * [5.1.2 Ejecución en paralelo individual](5.1.2-Ejecución-en-paralelo-individual)
        * [5.1.3 Ejecución en paralelo por grupo](5.1.3-Ejecución-en-paralelo-por-grupo)
    * [5.2 Monitoreo de tareas](5.2-Monitoreo-de-tareas)
    * [5.3 Cancelación de tareas](5.3-Cancelación-de-tareas)
* [6. Errores de ejecución de tareas / jobs.](6.-Errores-de-ejecución-de-tareas-/-jobs.)
    * [6.1 error JOB XXXXXXXXX ON mn00P CANCELLED AT (DATE)](6.1-error-JOB-XXXXXXXXX-ON-mn00P-CANCELLED-AT-(DATE).)
    * [6.2 OOM_KILL EVENT. Some of the step tasks have been OOM Killed.](6.2-OOM_KILL-EVENT.-Some-of-the-step-tasks-have-been-OOM-Killed.)
    * [6.3 Segmentation fault (core dumped). Aborted (core dumped)](6.3-Segmentation-fault-(core-dumped).-Aborted-(core-dumped))

## 1. Creación de cuentas, solicitudes de horas de computo, CPUs y Storage.

### 1.1 Creación de cuentas

La creación de cuentas del NLHPC se puede clasificar en 2 grupos: 1) Usuarios nuevos sin conexión previa al NLHPC y 2) Usuarios que serán parte de un grupo ya existente en el NLHPC.

1. En el primer grupo de usuarios, la creación de cuentas se da de forma exclusiva a un/una PI
    (Investigador Principal) o investigadores jóvenes, quienes deberán rellenar el siguiente
    formulario con la información correspondiente: https://solicitudes.nlhpc.cl/.

2. En el caso de que el PI esté generando una cuenta para su grupo o equipo y requiera más de una
    cuenta, lo ideal es generar 1 cuenta de PI en https://solicitudes.nlhpc.cl/ y cuentas individuale
    s para cada miembro del grupo, es decir:

    a) 1 Cuenta de PI. <br>
    b) N Cuentas, 1 por cada miembro del Equipo (Team).

La recomendación principal al crear cuentas para un grupo es, idealmente, asignar un Nombre del Equipo de Investigación. Como ejemplos: CRG-LAB1, CRG_UOH o, en mi caso particular, Mathomics. Esto facilitará la posterior creación de cuentas para miembros del mismo grupo y la asignación de permisos, protocolos y herramientas (tools) que el grupo completo necesitará eventualmente.

La recomendación principal es que cada nueva cuenta sea creada o solicitada por un solo miembro de cada Equipo o Grupo. Esta tarea puede recaer directamente en el PI o en un encargado seleccionado.

Para mantener el orden y la trazabilidad de los datos, lo ideal es que cada usuario pueda acceder a una sola cuenta. Compartir claves conlleva una alta probabilidad de accesos no autorizados, uso de recursos no controlados o eliminación de datos sin consentimiento. En el caso de necesitar una cuenta de datos que será utilizada solo por periodos cortos de tiempo por varios usuarios distintos, se recomienda crear una cuenta especial de invitado. Esta cuenta debe estar registrada con el mismo PI y bajo el mismo Equipo. Por lo general, estas cuentas se usan solo para compartir datos con otros investigadores o estudiantes en práctica que no necesitan cuentas permanentes individuales.

### 1.2 Solicitudes de horas de computo.

Durante la creación de la cuenta del PI, se requerirá establecer una cuota de horas de cómputo. Esta solicitud se asignará como límite de ejecución de tareas con una duración de 1 año, a partir de la fecha de la primera solicitud. Estas horas de cómputo se establecerán como límite para cada Equipo, por lo que no es necesario generar una petición de horas de cómputo por cada cuenta.

En el caso de que las horas de cómputo se cumplan, ninguna cuenta del Equipo podrá seguir ejecutando tareas hasta generar una nueva solicitud en https://solicitudes.nlhpc.cl/. Por lo general, una solicitud de horas de cómputo deberá tomar en cuenta la cantidad de miembros, las tareas que se necesitan ejecutar y la cantidad de veces que se necesita ejecutar la misma tarea. Como un buen estimador en bioinformática, la cantidad de horas para limpiar, ensamblar, anotar y analizar genomas durante 1 año calendario es de entre 20.000 y 50.000 horas por cuenta.

En el caso de cuentas con gran volumen de datos y varios análisis al año, las horas por cuenta pueden superar fácilmente las 250.000 horas de cómputo. La recomendación es:

    * Para Equipos nuevos: entre 10.000 a 15.000 horas de cómputo por cuenta.

    * Para Equipos con experiencia: entre 50.000 a 70.000 horas de cómputo por cuenta.

En el caso de que la cantidad de horas de cómputo solicitadas sea muy por debajo de lo necesario por cada Equipo, el equipo de Soporte del NLHPC enviará un correo a cada cuenta con la notificación de que el número de horas está por acabarse o completamente utilizado. En esta notificación, cada cuenta tendrá desglosado el número de horas que se utilizaron.

Para no repetir una nueva solicitud de horas de cómputo cada 4 o 6 meses, lo ideal es utilizar la información obtenida en la notificación del NLHPC y reajustar la petición para que coincida con el periodo de 12 meses.

#### El cobro de horas de cómputo se realiza sobre el uso real, y no sobre las horas solicitadas en la creación de cuentas. ####
<br>
### 1.3 CPUs y Storage

Al crear una nueva cuenta en el NLHPC, si no se especifica la cantidad de recursos de CPU y Almacenamiento, cada cuenta tendrá por defecto 88 CPU y 120 GB de Almacenamiento (Storage).
En el caso de las CPU, esto significa que el usuario puede utilizar un máximo de 88 CPU al mismo tiempo durante procesos de ejecución. Es decir, si ejecutamos 3 procesos con 40 CPU cada uno:

      a) Proceso 1 con 40 CPU. Este proceso se ejecutará sin problemas, siempre y cuando existan recursos en el NLHPC. 
      b) Proceso 2 con 40 CPU. Este proceso se ejecutará sin problemas, siempre y cuando existan recursos en el NLHPC.
      c) Proceso 3 con 40 CPU. Este proceso no se podrá ejecutar hasta que el proceso a) o b) terminen. 

En el caso del Storage, este valor es el limite maximo con el cual podremos guardar nuestros archivos o tareas. Si se da la instancia de que nuestra cuota de Storage esta en su limite, no se podran seguir ejecutando tareas, aun teniendo CPUs y horas de computo disponible. 
En el caso de que lleguemos al limite del Storage, durante la ejecución de una de nuestras tareas, esta terminara antes forzosamente, y se notificara al usuario de la falta de espacio en nuestra cuenta.

#### Tanto la cantidad de CPU como el Almacenamiento se pueden solicitar de forma individual para cada cuenta/usuario, por lo que es necesario revisar los requerimientos de cada uno. ####

A modo general el uso de recursos optimo es alrededor de:

    100 CPUs y 500Gb para Team nuevos. 
    200+ CPUs y 1Tb+ de Storage para Teams antiguos 

<br>
<br>

## 2. Login al NLHPC.
<br>
Una vez creada nuestra cuenta, podemos acceder al Login del NLHPC. El proceso actual, con fecha 2025, es el siguiente:

```
ssh -p 4603 mi_cuenta@leftraru.nlhpc.cl
```

Con este comando podremos entrar al NLHPC en cualquier parte del país, sin necesidad de una VPN.
En el caso de encontrarnos temporalmente en el extranjero, se deberá utilizar una VPN para anclarnos primero a Chile y luego acceder al servidor de manera normal.

<br>
<br>

## 3. Instalación de software mediante gestor de paquetes, Modo SUDO y Module LOAD.<br>

### 3.1 Instalación de software mediante gestor de paquetes
La mayoría de las herramientas (tools) y paquetes en Bioinformática se pueden encontrar en gestores de paquetes altamente utilizados en ciencia, tales como:
```
Anaconda3
Miniconda
Mamba
HomeBrew
PERL
PIP
```
Tanto Anaconda3 como Miniconda funcionan sin problemas en el NLHPC (https://www.anaconda.com/docs/getting-started/miniconda/install#linux-x86) y se pueden instalar de manera local en nuestra cuenta así:

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash ~/Miniconda3-latest-Linux-x86_64.sh
source ~/.bashrc
```
Una vez instalados, es tan simple como instalar cualquier herramienta que exista en el gestor de paquetes. En nuestro caso, usaremos como ejemplo **Meme Suite**. (https://anaconda.org/bioconda/meme):

```
conda install bioconda::meme
conda install bioconda/label/cf201901::meme
```

Eventualemte, la instalación se ejecutara sin problemas y podremos utilizar la herrameinta como corresponda.<br>

### 3.2 Modo SUDO

En el caso de nuestros computadores personales, podremos acceder a la instalación de tareas mediante SUDO o superusuario.
Este método de instalación está restringido para todas las cuentas del NLHPC a excepción del equipo de soporte, por lo que ninguna herramienta se podrá instalar mediante este método; es decir, los comandos tales como:

```
sudo install tool
sudo apt install tool
```
NO son validos.<br>
En el caso de necesitar instalar una herramienta que requiera específicamente este comando, existen 2 soluciones específicas:.<br>

#### A. Instalación local con el codigo fuente. ####

Para la instalación local de nuestra herramienta, primero necesitaremos el código fuente de la misma. Por lo general, cualquier herramienta que utilice el comando SUDO tiene un código fuente, el cual se puede descargar desde la página web del software o desde GitHub. En nuestro caso, seguiremos el ejemplo de MEME Suite (https://web.mit.edu/meme/current/share/doc/install.html):

```
tar zxf meme_4.11.4.tar.gz
cd meme_4.11.4
./configure --prefix=$HOME/meme --with-url=http://meme-suite.org --enable-build-libxml2 --enable-build-libxslt
make
make test
make instal
```

En el ejemplo anterior, podemos instalar localmente nuestra herramienta utilizando el comando específico:
```
--prefix=$HOME/my_carpeta_personal
o
--prefix=/home/my_cuenta/my_carpeta_personal
```

En el caso de que no exista la opción de instalación del código fuente, o encontremos errores dentro del proceso, podemos utilizar la opción B.<br>
#### B. Solicitud de instalación al equipo de Soporte NLHPC ####

Cada vez que necesitemos instalar herramientas que parecen demasiado complicadas o requieren librerías que no podemos encontrar, lo mejor es realizar una solicitud al equipo de Soporte del NLHPC (soporte@nlhpc.cl) mediante un correo.
```
at@ soporte@nlhpc.cl
Asunto: Instalacion tool Meme Suite:
_______________________________________

Correo.....

```
En nuestro correo de solicitud debemos agregar:

> El *link de la tool* a instalar. <br>
> El o los *usuarios* a los que se desea instalar la tool.

En el caso de que nuestra tool sea requerida por todo nuestro Team, existe la posibilidad de implementar la herramienta como Modulo, y que quede en el registro de tools instaladas del NLHPC para que pueda ser cargada por cualquier usuario, inclusive fuera de nuestro Team.
<br>

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

## 4. Archivo de ejecución de tareas / Jobs en la cola de procesos y solicitud de recursos .<br>

### 4.1 Archivo de ejecución de tareas / Jobs <br>

Todas las tareas que necesitemos ejecutar en el NLHPC deben entrar en la cola de procesos a través de un archivo de ejecución.
Ejecutar tareas directamente en la consola, sin pasar por la cola de procesos, tiene un tiempo límite máximo de ejecución de 30 minutos.
Lo ideal es siempre utilizar la cola de procesos, puesto que correr directamente desde la consola utiliza los recursos del sistema de login, lo cual ralentiza toda la navegación en el sistema NLHPC.

Tareas pequeñas como parsear archivos, uso de grep o awk se pueden realizar perfectamente en la consola de login. Tareas como ensambles, anotaciones u otras que requieran más de una CPU o bastante memoria RAM están prohibidas.

En el caso que requiramos ejecutar una tarea en la cola de procesos, necesitaremos un archivo de ejecución. A continuación, tendremos uno básico que nos servirá para la mayoría de nuestras tareas.

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
#SBATCH -o [OUTPUT FILE] 
#SBATCH -e [ERROR FILE]
#SBATCH -t [EXECUTION TIME]
#SBATCH --mail-user=your-email-here@examp.com
#SBATCH --mail-type=ALL

Aca-nuestro-programa

```
<br>

### Revisemos ahora cada uno de los parametros: ####

<br>


```
#SBATCH -J [JOB_NAME] :           Aquí irá el nombre de nuestra tarea. Utilizar nombres cortos y fáciles de identificar
                                  es lo recomendado.
```

```
#SBATCH -p [PARTITION] :          En este campo irá la partición del NLHPC a la cual enviaremos nuestra tarea. Actualmente,
                                  existen 6 particiones que los usuarios pueden utilizar. Las características de cada
                                  partición se encuentran en https://dashboard.nlhpc.cl/.
                                  Estas particiones son:
                                  main,
                                  general,
                                  largemem,
                                  mi210,
                                  mi100,
                                  v100.
                                  Se deberá escoger la partición según las necesidades que tengamos para ejecutar
                                  nuestras herramientas. La mayor parte de nuestras tareas correrán en "general",
                                  "main" o "largemem", puesto que CPU y RAM componen la mayor parte de las herramientas
                                  en Bioinformática.

```


```
#SBATCH -n [NUMBER OF NODES]:     Este parámetro indica el número de NODOS para ejecutar nuestras tareas.
                                  En Bioinformática, muy pocas herramientas están optimizadas para ejecutarse en más
                                  de 1 NODO, por lo que es prácticamente improbable utilizar más de 1
```



```
#SBATCH -c [NUMBER OF CPU] :      Aquí se establece el número de CPU a utilizar. Por más que podamos pedir 100 CPU, la mayor
                                  parte de las herramientas en Bioinformática solo escalan hasta 12 o 20 CPU, con algunas
                                  excepciones llegando a los 40 CPU. Pedir más no nos dará una ventaja real de tiempo de
                                  ejecución. Al contrario, perderemos más tiempo esperando que se liberen los recursos que
                                  ejecutar las tareas con la mitad de CPU. Formato: Números enteros del 1 al 256, dependiendo
                                  de cada partición:
                                  Límite CPU partición main = 256;
                                  Límite CPU partición general = 44;
                                  Límite CPU partición largemem = 44.
```


```
#SBATCH --mem= [RAM MEMORY IN GB] :Este parámetro reserva la cantidad de memoria RAM que necesitará nuestra herramienta.
                                  La cantidad de RAM se debe establecer en relación al NODO que se está reservando;
                                  es decir, no es posible reservar 200 GB de RAM en la partición "general" ni 1 TB de RAM
                                  en la partición "largemem". El equipo del NLHPC recomienda utilizar a lo máximo 5 GB de
                                  RAM por CPU, aunque esta recomendación es casi inutilizable en Bioinformática.
                                  En nuestro caso, existirán herramientas que utilizarán 200 a 400 GB de RAM, pero se
                                  ejecutarán solo en 20 a 40 CPU.
                                  Más adelante veremos algunos ejemplos de ejecución. Formato: Números enteros del 1 al 710,
                                  seguido del sufijo GB, dependiendo de cada partición:
                                  Límite RAM partición main = 710 GB;
                                  Límite RAM partición general = 175 GB;
                                  Límite RAM partición largemem = 710 GB

   
```

```
#SBATCH -o [OUTPUT FILE] :        Este archivo contiene la salida por consola de nuestra herramienta. Cuando la
                                  herramienta que estamos tratando de ejecutar no tiene configurado un archivo de output,
                                  la salida de nuestro programa será escrita aquí. La mayor parte de los archivos output
                                  será un mensaje propio de cada herramienta con información y tiempo de ejecución.
```

```
#SBATCH -e [ERROR FILE] :         Este archivo contendrá la salida de errores de la ejecución de nuestra herramienta.
                                  Aquí podremos revisar si nuestra ejecución fue exitosa o si existió algún problema
                                  particular que produjo la terminación forzosa de nuestro job. Es importante siempre
                                  configurar este archivo, pues es la única forma real de reconocer errores para futuras
                                  ejecuciones. (Nota: Intercambié la descripción de -o y -e ya que -e suele ser
                                  Error estándar).
```

```
#SBATCH -t [EXECUTION TIME] :     Este parámetro ha sido recientemente introducido en el año 2025 y reserva el tiempo de
                                  ejecución de nuestra tarea. No es necesario ser extremadamente exacto en los tiempos de
                                  ejecución, pero generalmente podemos utilizar horas o días sin mayores cambios de esta
                                  variable. Si nuestra tarea supera el tiempo reservado, esta se cancelará automáticamente
                                  y tendremos que volver a lanzarla desde el inicio. Formato: dd-hh:mm:ss.
                                  Ejemplo para 1 día, 3 horas y 20 minutos de ejecución sería: 1-03:20:00.
```
```
#SBATCH --mail-user=your-email-here@examp.com : Opcional. Generará un correo automático con información de nuestra tarea.  
#SBATCH --mail-type=ALL                       :  Opcional. Indica que envíe correo en todos los estados (BEGIN, END,
                                                 FAIL, etc.).
                                                
```

<br>


Ahora que ya sabemos como configurar nuestro archivo de ejecución, veamos un ejemplo real.
   
```
#SBATCH -J GBK
#SBATCH -p general
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=6GB
#SBATCH -o error.%a.%N.%j.out 
#SBATCH -e error.%a.%N.%j.err
#SBATCH -t 06:00:00
#SBATCH --mail-user=your-email-here@examp.com
#SBATCH --mail-type=ALL

python gbk_generator.py my_input_1 my_input_2 > salida_programa.tsv

```

<br>



### 4.2 Solicitud de Recursos ###

Una vez revisado cada campo de nuestro Archivo de ejecución de tareas, podremos ahora solicitar la cantidad de recursos y el tiempo que estimemos conveniente. 
Como se mencionó brevemente, una herramienta que pueda utilizar más de 1 CPU no necesariamente se ejecutará 70 veces más rápido al pedir 70 CPU.

La experiencia nos dice que la mayor cantidad de herramientas grandes escala solo hasta los 20 a 40 CPU. Además, es mucho más eficiente dividir nuestras tareas en fragmentos o chunks y ejecutarlos al mismo tiempo, que ejecutar todo junto pidiendo más CPU;
es decir, ejecutar la misma tarea, dividida en 5 partes con 20 CPU cada una, será mucho más eficiente que ejecutar la misma tarea completa 1 vez con 100 CPU.

De todas formas, existe un catálogo infinito de herramientas que podremos utilizar, y aunque no podemos conocer a priori sus requerimientos de ejecución de máxima eficiencia, la experiencia nos brindará un mejor juicio a la hora de escoger recursos.
<br>
Pero a falta de tiempo, he aquí algunos ejemplos:

### TAREAS DE ASSEMBLY. 1 Metegenoma grande de 200+ Millones de Reads. Tool: MEGAHIT ###

```
#SBATCH -J Assembly
#SBATCH -p main o largemem
#SBATCH -n 1
#SBATCH -c [12-20]
#SBATCH --mem=[200GB-400GB]
#SBATCH -t 2-00:00:00
```

### TAREAS DE ANOTACION.  Mismo metagenoma, contra una base de datos de 50GB. Tool: EggNOGMapper ###

```
#SBATCH -J annotation
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [8 a 12]
#SBATCH --mem=80GB
#SBATCH -t 4-00:00:00
```

### CLUSTERING DE GENES.  400+ Millones de CDS. Tool: MMseqs2 ###

```
#SBATCH -J cluster
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [12 a 20]
#SBATCH --mem=[400GB - 500GB]
#SBATCH -t 3-00:00:00
```

### CREACION DE MAGS / BINNING. Tool: SemiBin2 ### 

```
#SBATCH -J binning
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [12 a 20]
#SBATCH --mem=[20GB - 150GB]
#SBATCH -t [2-00:00:00 a 7-00:00:00]
```

### ANOTACION DE MAGS. 1 MAG. Tool: Bakta: ###

```
#SBATCH -J mag_annot
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c 2
#SBATCH --mem=20GB
#SBATCH -t 08:00:00
```

### ANOTACION DE MAGS. 1000+ MAG. Tool: DRAM: ###

```
#SBATCH -J mag_annot
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c [12 a 20]
#SBATCH --mem=200GB
#SBATCH -t 14-23:00:00
```

### PARSEO DE BASES DE DATOS / SCRIPTS DE PYTHON, ENTRE OTROS: ###

```
#SBATCH -J job
#SBATCH -p general o main
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=[5GB - 40GB]
#SBATCH -t [06:00:00 a 1-00:00:00]
```


Estos son algunos ejemplos de las tareas con mayor cantidad de recursos que he tenido experiencia de probar en el NLHPC. Cabe considerar que estos datos tienen un peso aproximado de TBs, 
por lo que proyectos relativamente livianos requerirán menos recursos. Cabe destacar que la regla de 1 CPU por cada 5 GB de RAM no aplica para ninguno de los programas listados.
Esta regla es más bien una recomendación de eficiencia en programas altamente revisados y, lamentablemente, no aplica para la mayoría de herramientas bioinformáticas. 
Mientras utilicemos rangos de CPU y RAM que no se salgan de extremos, como por ejemplo, ejecutar una herramienta single thread con 50 CPU y 700 GB de RAM, no deberíamos tener mayores problemas.

###########################################################################################################
## IMPORTANTE ##
#### Todas las tareas / jobs, tienen un maximo tiempo de ejecucion de 30 DIAS. Luego de esto, sin importar el tiempo pedido, la tarea sera cancelada automaticamente ####

###########################################################################################################

¿Y qué hacemos si nuestra herramienta necesita correr por más de 30 días y no queremos que se cancele automáticamente?

Para estas excepciones y otras, podemos enviar un correo a soporte@nlhpc.cl y enviar nuestro *JOB_ID* de la tarea en ejecución para pedir una extensión de tiempo.

<br>
<br>

## 5. Ejecución de tareas / jobs, Monitoreo de tareas y Cancelación de tareas <br>

### 5.1 Ejecución de tareas


Una vez que ya tenemos creado nuestro archivo de ejecución de tareas y alocado nuestros recursos, debemos ahora lista y ejecutar nuestras tareas.

Para ello, tomaremos nuevamente nuestro archivo de ejemplo.


```
#SBATCH -J python_script
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=[10GB - 50GB]
#SBATCH -t 1-00:00:00

python my_tool.py my_input_file.tsv > output_one.tsv

python my_second_tool.py output_one.tsv > output_two.tsv

echo "Task Completed"


```
En este caso, nuestro archivo de ejecución tratara de ejecutar un script de python llamado my_tool.py y este a su vez requerira un archivo de entrada llamado my_input_file.tsv. Este script generara un arvhivo de salida output_one.tsv que sera utilizado ahora como input por nuestro segundo script my_second_tool.py y generara la salida final output_two.tsv.

Como se puede observar, se pueden listar mas de una ejecución o linea de comando en nuestro archivo de ejecución de tareas, done incluso podremos construir pipelines completos para tareas especificas.

Una vez que tengamos todos los comandos a ejecutar, guardaremos nuestro archivo de ejecución, en este caso, nuetro ejemplo se llamará, standar.sh

```
standar.sh

```

Para poder ejecutar ahora nuestros comandos dentro del archivo standar.sh, lo que debemos hacer es llamar en la consola a la función sbatch con el nombre de nuestro archivo de ejecución y luego presionar enter.

```
$ sbatch standar.sh
```

Si nuetro archivo de ejecucioón esta correcto, nos aparecera el mensaje:

```
Submitted batch job XXXXXXXXXXXXXXX
```

Este numero de job es importante, puesto que nos permitira rastrear el status de nuestra tarea a futuro.

Pero, ¿Que pasa si quiero ejecutar mas de 1 tarea al mismo tiempo?

En este caso, tenemos varias opciones. 

#### 5.1.1 Ejecución lineal

Para este tipo de ejecución, solo debemos escribir todos nuestros comandos juntos en el mismo archivo de ejecución de tareas, cada ejecución debajo de la siguiente, es decir:

```
#SBATCH -J python_script
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=[10GB - 50GB]
#SBATCH -t 4-00:00:00

#Primera ejecución

python my_tool.py my_input_file_1.tsv > output_one_1.tsv
python my_second_tool.py output_one_1.tsv > output_two_1.tsv

# Segunda ejecución

python my_tool.py my_input_file_2.tsv > output_one_2.tsv
python my_second_tool.py output_one_2.tsv > output_two_2.tsv

# Tercera ejecución

python my_tool.py my_input_file_3.tsv > output_one_3.tsv
python my_second_tool.py output_one_3.tsv > output_two_3.tsv

# Cuarta ejecucióm

python my_tool.py my_input_file_4.tsv > output_one_4.tsv
python my_second_tool.py output_one_4.tsv > output_two_4.tsv

echo "Task Completed"

```

Con este tipo de archivo de ejecución, todas las tareas se ejecutaran de manera linea, y cada comando debera esperar al anterior para ser ejecutado. Si bien es cierto, esta el la mejor forma para generar pipelines, no es muy eficiente si queremos ejecutar la misma tarea muchas veces. 

###########################################################################################################
## IMPORTANTE ##
#### 
Hay que recordar que si 1 sola tarea toma 1 dia en ejecutarse, ahora tendremos que solicitar 4 veces mas tiempo de ejecución. ####

###########################################################################################################

Pero que pasa si nuestros tiempo de ejecución son demasiado largos? es necesario esperar 7 dias por 7 ejecuciones?. Ahora veremos soluciones a este problema.

#### 5.1.2 Ejecución en paralelo individual

En esta ocasión modificaremos nuestro archivo de ejecución de tareas para poder hacer uso del traspaso de nombres de variables por consola, y asi, generalizar nuestros scripts.

```
#SBATCH -J python_script
#SBATCH -p main
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=[10GB - 50GB]
#SBATCH -t 1-00:00:00

#Ejecución estandar

python my_tool.py $1.tsv > $2.tsv
python my_second_tool.py $2.tsv > $3.tsv
```

En esta versión del script, hemos reemplazado los nombres originales, donde ahora, hemos generalizado los nombres my_input_file_N.tsv a $1, asi tambien como los archivos output_one_N.tsv por $2 y output_two_N.tsv por $3.

Con ello ahora nuestra llamada al archivo de ejecución de tareas cambiara de la siguiente forma:

```
# Antiguo metodo de ejecución
$ sbatch standar.sh

# Nuevo metodo de ejecución
$4 sbatch standar.sh my_input_file_N.tsv output_one_N.tsv output_two_N.tsv
```

Es aquí donde podemos observar la mayor ventaja del método paralelo. El unico limite de numero de tareas a llamar sera la cantidad de CPU que nuestra cuenta tenga acceso, por lo que ahora, nuestras 4 llamadas de scripts anteriores cambiará a:

```
$ sbatch standar.sh my_input_file_1.tsv output_one_1.tsv output_two_1.tsv
Submitted batch job 000001
$ sbatch standar.sh my_input_file_2.tsv output_one_2.tsv output_two_2.tsv
Submitted batch job 000002
$ sbatch standar.sh my_input_file_3.tsv output_one_3.tsv output_two_3.tsv
Submitted batch job 000003
$ sbatch standar.sh my_input_file_4.tsv output_one_4.tsv output_two_4.tsv
Submitted batch job 000003
```
Este metodo asegurara ahora que podamos ejecutar nuestras 4 tareas al mismo tiempo, por lo que el tiempo de ejecución pasara de 4 dias, a 1 solo dia en el mejor de los casos (en el caso de que tengamos los recursos y sean asignados a nuestra cuenta).

Pero ¿Que pasa si necesitamos ejecutar 100 tareas o 1000 tareasd el mismo tipo? ¿Tendremos que escribir 100 o 1000 veces en la consola los nombres de nuestros archivos?

#### 5.1.3 Ejecución en paralelo por grupo

La diferencia entre la la ejecución en pararelo individual y en grupo es solo 1, como manejamos la manea de llamar 100 o 1000 tareas al mismo tiempo.

Para esta tarea, podemos usar el mismo archivo standar.sh anterior, por lo que aca no habran cambios, la unica diferencia es la llamada del archivo de ejecución. Para ello, generaremos un archivo BASH con todas las llamadas de ejecución que necesitemos realizar y ejecutaremos este archivo automático, es decir.


```
# Antiguo metodo de ejecución
$ sbatch standar.sh my_input_file_1.tsv output_one_1.tsv output_two_1.tsv
Submitted batch job 000001
$ sbatch standar.sh my_input_file_2.tsv output_one_2.tsv output_two_2.tsv
Submitted batch job 000002
$ sbatch standar.sh my_input_file_3.tsv output_one_3.tsv output_two_3.tsv
Submitted batch job 000003
$ sbatch standar.sh my_input_file_4.tsv output_one_4.tsv output_two_4.tsv
Submitted batch job 000003
```

Nuevo metodo de ejecución.

1. Crear un archivo de grupo de ejecución
```
vim group_1.sh
```
2. Dentro del archivo de grupo de ejecución, escribiremos todas nuestras tareas. Dado que lo unico que cambia es el nombre de input, podemos utilizar un script simple de AWK, python o EXCEL para poder generar las llamadas.
```
sbatch standar.sh my_input_file_1.tsv output_one_1.tsv output_two_1.tsv
sbatch standar.sh my_input_file_2.tsv output_one_2.tsv output_two_2.tsv
sbatch standar.sh my_input_file_3.tsv output_one_3.tsv output_two_3.tsv
sbatch standar.sh my_input_file_4.tsv output_one_4.tsv output_two_4.tsv
sbatch standar.sh my_input_file_5.tsv output_one_5.tsv output_two_5.tsv
sbatch standar.sh my_input_file_N.tsv output_one_N.tsv output_two_N.tsv
```
3. Finalmente llamaremos al archivo de grupo de ejecución y automaticamente, todas las llamadas se ejecutaran al mismo tiempo.
```
bash group_1.sh
```
4. Lo que veremos ahora como respuesta en la consola, sera algo como
```
Submitted batch job 000001
Submitted batch job 000002
Submitted batch job 000003
Submitted batch job 000004
Submitted batch job 000005
Submitted batch job 00000N
```

###########################################################################################################
## IMPORTANTE ##
#### ¿Cuántas llamadas podría ejecutar al mismo tiempo? ####
###########################################################################################################

Por lo general, se utilizan llamadas de entre 50 a 100 tareas por cada archivo de ejecución de grupo, por lo que es necesario separar llamadas de mas de 100 tareas en grupos de este tamaño. En el caso de tener 500 tareas, generar 5 archivos con grupos de 100 llamadas seria óptimo.
<br>

### 5.2 Monitoreo de tareas

Monitorear tareas es bastante simple, para ello podemos utilizar 2 comandos especificos. 
El primero es:

```
$ squeue
```
Este comando nos dara una mirada rápida para revisar las tareas que enviamos a ejecutar y cual es su estado actual.
Si ejecutamos este comando, y acabamos de lanzar nuestras tareas, podremos observar lo siguiente.
```
JOBID    PARTITION            NAME          USER        ST    TIME    NODES    NODELIST(REASON)
000001        main    python_script   [your_user] [status]    0:00        1    [REASON:NODE_ID]
000002        main    python_script   [your_user] [status]    0:00        1    [REASON:NODE_ID]
000003        main    python_script   [your_user] [status]    0:00        1    [REASON:NODE_ID]
000004        main    python_script   [your_user] [status]    0:00        1    [REASON:NODE_ID]
000005        main    python_script   [your_user] [status]    0:00        1    [REASON:NODE_ID]
00000N        main    python_script   [your_user] [status]    0:00        1    [REASON:NODE_ID]
```

El segundo comando es:

```
$ watch squeue
```
Este comando nos permitira tener una ventana permanente que se actualizará cada 2 segundos, entregandonos información en tiempo real de nuestras tareas.
La informacón mostrada, sera exactamente la misma a la anterior.

Revisemos ahora la información entregada:

```
JOBID:              Contiene el ID de nuestra tarea, este sera el mismo ID mencionado
                    al ejecutar nuestra tarea.
PARTITION:          Contiene el nombre de la partición donde ejecutamos nuestra tarea.  
NAME:               Nombre de nuestra tarea.
USER:               Nombre de nuestro usuario.
ST:                 Estatus del job que hemos enviado, estos pueden ser:
                    PD: Nuestra tarea esta pendiende de ejecución (pending)
                    R:  Nuestra tarea se esta ejecutando (running)
                    CG: Nuestra tarea esta terminando (completing)
TIME:               Contiene el tiempo de ejecución de nuestra tarea.
NODES:              Numero de nodos asignados a nuestra tarea.
NODELIST(REASON):   Nodo en el cual se esta ejecutando nuestra tarea. En en caso de que
                    nuestra tarea se encuentre en el estatus pendiente: (ST : PD ), esta
                    columna desplegará la razón del porque esta pendiente.
                    Resources: Nuestra tarea esta esperando que un nodo tenga los recursos
                    que solicitamos para poder ejecutarse.
                    Priority: Nuestra tarea esta en la cola de procesos y esta esperando
                    a que tareas de otros usuarios terminen
                    QOS[MaxCPULimit]: Nuestra cuenta ya esta utilizando el Maximo numero
                    de CPU asignados a nuestro usuario y tendremos que esperar a que otras
                    de nuestras tareas terminen
```

<br>

### 5.3 Cancelación de tareas

En el caso de que necesitemos cancelar o terminar forzosamente una tarea (error en el script, error en el uso de recursos, etc), podremos cancerlar solo usando su JOBID mencionado anteriormente, para ello, podremos utilizar el comando:

```
$ scancel [JOBID]

Ejemplo:
$ scancel 000001
```

Con esto, podemos eliminar esta tarea de la cola, y volver a relanzar nuestro script con las modificaciones que necesitemos.



<br>
<br>

## 6. Errores de ejecución de tareas / jobs. <br>

En un mundo perfecto, todas nuestras tareas correrán en el tiempo asignado y finalizarán sin ningún inconveniente. Mientras eso no exista, revisemos algunos de los errores más frecuentes y cómo solucionarlos.

### 6.1 error JOB XXXXXXXXX ON mn00P CANCELLED AT (DATE). ###

Este error es frecuentemente encontrado cuando nuestra tarea está subutilizando recursos y es cancelada automáticamente por el sistema.
Este caso se da si pedimos demasiados CPU o RAM, pero nuestra tarea está utilizando menos del 20% de los recursos solicitados.

Si configuramos correctamente nuestro correo en el archivo de Ejecución de tareas, podremos recibir un correo del NLHPC (por lo general a la bandeja de spam) con el mensaje:

```
[NLHPC] - Aviso de Subutilización de Recursos (MEM):

o

[NLHPC] - Aviso de Subutilización de Recursos (CPU):
```

Con este correo, podemos verificar el comportamiento de nuestra tarea y corregir la solicitud de recursos a una más apropiada.
<br>

###########################################################################################################
## IMPORTANTE ##
#### ¿Qué pasa si estoy pidiendo solo 1 CPU y 1 GB de RAM y aun así mi tarea se está cancelando por subutilización de recursos? ¿Qué pasa si mi tarea se ejecuta con los recursos correctos durante las primeras horas, pero luego subutiliza recursos? ####

###########################################################################################################

Para este tipo de casos, debemos enviar un correo a soporte indicando nuestro problema. Luego se nos pedirá ejecutar la tarea nuevamente y enviar el JOB_ID para que esta tarea sea excluida de la cancelación automática y entre a la "White List" de procesos.


<br>

### 6.2 OOM_KILL EVENT. Some of the step tasks have been OOM Killed. ###

```
check.XXXXXXXXXmn00P.NNNNNNNNN.err:slurmstepd: error: Detected 1 oom_kill event in StepId=XXXXXXXXXX.batch.
Some of the step tasks have been OOM Killed.

o

Detected 1 oom-kill event(s) in StepId=XXXXXXXX.batch.
Some of your processes may have been killed by the cgroup out-of-memory handler.
```

Este será uno de los principales errores que encontraremos a diario en nuestro archivo #SBATCH -e [ERROR FILE]. Este error indica principalmente que la cantidad de RAM que solicitamos es insuficiente y debemos pedir más en nuestro Archivo de ejecución.
Existen algunas herramientas que recomiendan un número definido de RAM, pero para la mayoría, seremos nosotros los que decidamos cuánta memoria solicitar. **Como buena práctica, incrementar la RAM en un 20% extra e intentar nuevamente suele ser la mejor opción**

<br>

### 6.3 Segmentation fault (core dumped). Aborted (core dumped) ###

```
/tmp/10781177854440103180/linclust/3581267220862219892/linclust.sh:
line 76: 1624213 Segmentation fault (core dumped) 
```

Este error no es grave, es gravísimo, al borde de lo radiactivo y letal. Significa que, en el NODO donde estamos ejecutando nuestra tarea, una de las herramientas siendo ejecutadas hizo que el NODO completo colapsara y dejara de correr todas las tareas. Este es un fallo catastrófico como el famoso "pantallazo azul" en Windows. Es de vital importancia revisar el archivo de errores y la ejecución de la tarea para saber si fue nuestra herramienta la que generó el fallo u otra que estaba ejecutándose junto a la nuestra en el mismo NODO. Como se podrá asumir, este error termina forzosamente todas las tareas del NODO en que se estaba ejecutando, lo que no solo nos afecta a nosotros, sino al resto de los usuarios.

En el caso de que relancemos nuestra tarea, y este error vuelva a ocurrir, habrá que comunicarse con soporte@nlhpc.cl y pedir el uso exclusivo de un NODO, así como el monitoreo extenso de nuestro job. Así, podemos ver cómo solucionar el problema. En el peor de los casos, no podremos seguir ejecutando nuestro programa. En el mejor de los casos, y mayoritariamente por experiencia, bajar el número de CPU y aumentar la RAM elimina satisfactoriamente este error. El tiempo de ejecución aumentará, pero es mejor terminar más tarde que no terminar. En otras ocasiones, hay herramientas que por defecto, internamente llaman a más de 1 CPU para tareas secundarias, por lo que es esencial conocer los requerimientos internos de cada ejecución. Este tipo de requerimientos fallidos también puede provocar un "core-dumped".





