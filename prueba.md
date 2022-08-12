# INCOMING MULTIBANK
## Objetivo 🎯
_Procesamiento y traslado de archivos incomming visa y mastercard._

## Documento de definición del proceso 📃: 
https://alignet.atlassian.net/wiki/spaces/TI/pages/2430042128/DDP-+Procesamiento+de+archivos+Incoming+LEGACY

## Comenzando  🚀

_Estas instrucciones te permitirán obtener una copia del proyecto en funcionamiento en tu máquina local para propósitos de desarrollo y pruebas._


### Pre-requisitos  📋
-  _Tener instalado y configurado aws-cli_
-  _Tener instalado Git_
-  _Tener instalado Python_
- _Crear un archivo .env con todas las variables de entorno para desarrollo_

```
SECRET_RPA_INCOMING_MULTIBANK  = dev/rpa-incoming-multibank

SECRET_MICROSOFT_GRAPH  = dev/secretos-microsoft-graph

NAME_REGION  = us-east-1

DIRECTORIOS  = D:/IBM/Apps/SPI/ACQ13/PR/,D:/IBM/Apps/SPI CARGA/VISA/

SERVER_HOST  = 172.19.46.153

SENDER  = operacionesrpa@alignet.com

SMTP_SERVER  = mail.smtp2go.com

SMTP_PORT  = 2525

EMAIL_PAGERDUTY  = miguelaurente1@gmail.com

HOST_SFTP  = 172.19.46.154

EMAIL_TO_SEARCH  = cos@alignet.ws

KEY_TO_SEARCH  = ARCHIVO INCOMIN

RUTA_SFTP_CREDIMATIC  = /Alignet/archgenerados/
```
- _Instalar pipenv para gestion de entornos virtuales_
	```
	pip install pipenv
	```
### Instalación  🔧

_El siguiente comando crea un entorno virtual y configura las variables de entorno del archivo .env_
```
pipenv shell
```
![enter image description here](http://drive.google.com/uc?export=view&id=1T83KeetRbNpIyn0jEaeS4NTmSK8Ztq_f)
_instalar dependencias_

```
pipenv install
```

_Ejemplo_

![enter image description here](http://drive.google.com/uc?export=view&id=1i-pa5nTYHXXc4u_IJcinA1VO8ghav4ys)
## Ejecutando las pruebas  ⚙️

_para ejecutar pruebas de debe seguir los siguientes pasos:_

 - Alojar archivos en la siguiente  ruta  **/Alignet/archgenerados/**
   ubicado en el servidor sftp de pruebas **(172.19.46.154)**
 - Dentro del servidor **173.19.46.153** borrar los archivos de la
   carpeta **D:\IBM\Apps\SPI\ACQ13\TA**  si en caso tiene.
 - En el servidor **172.19.46.153** Generar los siguientes archivos  o en todo caso cambiarles la fecha de creación de los archivos para simular la interaccion del spi.jar en la ruta
   ***D:/IBM/Apps/SPI/REPORTES/vpayment_files/download_files/acq13***
	```
	    MASTERCARD_INC_CHARGEBACK_20220411_001.pdf
	    MASTERCARD_INC_FEE_COLLECTION_20220411_001.pdf
	    MASTERCARD_INC_FUNDS_DISBURSEMENT_20220411_001.pdf
	    MASTERCARD_INC_RETRIEVAL_REQUEST_20220411_001.pdf
	    VISA_INC_CHARGEBACK_20220411_001.pdf
	    VISA_INC_FEE_COLLECTION_20220411_001.pdf
	    VISA_INC_FUNDS_DISBURSEMENT_20220411_001.pdf
	    VISA_INC_RETRIEVAL_REQUEST_20220411_001.pdf
	```
_Una vez hecho los pasos anteriores debe ejecutar el comando:_
```
python -m robot rpa_multibank_pt1.robot
```
Resultado:
![enter image description here](http://drive.google.com/uc?export=view&id=1mc3ebCj8uz12z70gbtDBD-A06IjsrICf)

Luego ejecute el siguiente comando:
```
python -m robot rpa_multibank_pt2.robot
```
_finalmente debe entregar el siguiente resultado:_

![enter image description here](http://drive.google.com/uc?export=view&id=1h4umOrILZgHZQ1mI1iNkQFJ8IfdqO0ej)
### Analice las pruebas end-to-end  🔩
#### Primera parte
Luego de ejecutar el comando
```
python -m robot rpa_multibank_pt1.robot
```

_Validación 1_ ✅

Ingresar a la servidor de pruebas **172.19.46.153** y verificar que los archivos descargados del correo sean trasladados a estas dos rutas:
 - [ ] D:/IBM/Apps/SPI/ACQ13/PR/
 
 - [ ] D:/IBM/Apps/SPI CARGA/VISA/
 
 _Validación 2_ ✅
 
Verificar que los archivos hayan sigo trasladados a las siguientes rutas del servidor de pruebas **172.19.46.153**
 - [ ] D:/IBM/Apps/SPI CARGA/MC/
 - [ ] D:/IBM/Apps/SPI/ACQ13/PR/

#### Segunda parte
Luego de ejecutar el comando
```
python -m robot rpa_multibank_pt2.robot
```
_Validación 1_ ✅

En el  servidor de pruebas **172.19.46.153**  verificar si los archivos son trasladados de **D:/IBM/Apps/SPI/REPORTES/vpayment_files/download_files/acq13**   ➡ **D:/IBM/Apps/SPI/ACQ13/TA**

_Validación 2_ ✅

En el  servidor de pruebas sftp **172.19.46.154**  verificar si los archivos han sido depositado en las rutas 

 - [ ] /ACQ13/TA
 - [ ] /ACQ13/PR

## Autores  ✒️

-   **Miguel Laurente Ccarhuachin**  
