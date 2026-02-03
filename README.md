
# SentinelDownloader

## Description
SentinelDownloader is an open source project to automatically download Sentinel-1, Sentinel-2, Sentinel-3 and Sentinel-5P user products (see available products below) from the [Copernicus Open Access Hub](https://scihub.copernicus.eu/) in an asynchronous fashion.

This package was developed as part of a project by the Inter-American Development Bank's Office of Strategic Planning and Development Effectiveness (SPD) to facilitate the use of satellite data towards improving the development effectiveness of IDB projects.

Once parameters have been specified, SentinelDownloader uses the [dhusget script](https://scihub.copernicus.eu/twiki/do/view/SciHubUserGuide/BatchScripting#dhusget_script) provided by Copernicus to first retrieve what are know as the _manifests_ - CSVs files that contain the URLs pointing to the locations of the requested products. After the manifests have been downloaded and read, the library asynchronously downloads the ordered files using AsyncIO, AIOfiles and AIOhttp.

## Environment

Create the environment to use SentinelDownloader with
```bash 
make create
```
To remove the environment, do
```bash 
make remove
```

## Usage

There are 3 ways you can use this package:

- ### Standard Python Library
    You can use this package as a standard Python library by specifying parameters and calling functions just as in the file _example_script.py_.
    To run, simply modify the script and then do 
    ```bash
    python example_script.py
    ```

- ### Through a YAML configuration file
    Set up the parameters in a YAML file (check the _configs_ folder) and then execute using the _run.py_ like 
    ```bash 
    python run.py config_run "configs/config.yaml"
    ```

- ### Command-line interface (CLI)
    You can run both package functions using the Fire CLI as shown below
  ```bash
  python run.py download_manifests --start_date '2022-09-01' --end_date '2022-09-05' --pipeline_name 'buenosaires' --manifests_dir 'manifests' --platformname 'Sentinel-5' --product 'L2__NO2___' --geom_wkt 'POLYGON((-61.2736 -32.3028, -54.0606 -32.3028, -54.0606 -35.8176, -61.2736 -35.8176, -61.2736 -32.3028))' --verbose True --processingmode 'NT' --username 's5pguest' --password 's5pguest'
  ```
  ```bash
  python run.py download_data --pipeline_name 'buenosaires' --manifests_dir 'manifests' --downloads_dir 'downloads' --username 's5pguest' --password 's5pguest'
  ```
## Parameters explanation
#### **```start_date``` & ```end_date```:**
Parameters for setting the time window for retrieving the files.
#### **```pipeline_name```:**
Name for the folder containing the files for that 'run'.
#### **```manifests_dir```:**
Name for the folder inside ```pipeline_name/``` for storing the manifests.
#### **```downloads_dir```:**
Name for the folder inside ```pipeline_name/``` for storing the satellite products. 
#### **```platformname```:**
Specifies the Satellite Platform name. Must be in the following:
- ```Sentinel-1```
- ```Sentinel-2```
- ```Sentinel-3```
- ```Sentinel-5```
#### **```product```:**
Specifies the product type for that Satellite Platform. Available products for each satellite:
| Mission               | Product type |
| ---------             | :-----------: |
| Sentinel-1            | SLC, GRD, OCN |
| Sentinel-2            | S2MSI2A,S2MSI1C, S2MS2Ap |
| Sentinel-3            | SR_1_SRA___, SR_1_SRA_A, SR_1_SRA_BS, SR_2_LAN___, OL_1_EFR___, OL_1_ERR___, OL_2_LFR___, OL_2_LRR___, SL_1_RBT___, SL_2_LST___, SY_2_SYN___, SY_2_V10___, SY_2_VG1___, SY_2_VGP___, SY_2_AOD__, SL_2_FRP__ |
| Sentinel-5            | L1B_IR_SIR, L1B_IR_UVN, L1B_RA_BD1, L1B_RA_BD2, L1B_RA_BD3, L1B_RA_BD4, L1B_RA_BD5, L1B_RA_BD6, L1B_RA_BD7, L1B_RA_BD8, L2__AER_AI, L2__AER_LH, L2__CH4, L2__CLOUD_, L2__CO____, L2__HCHO__, L2__NO2___, L2__NP_BD3, L2__NP_BD6, L2__NP_BD7, L2__O3_TCL, L2__O3____, L2__SO2___, AUX_CTMFCT, AUX_CTMANA |
#### **```geom_wkt```:**
Well-known text (WKT) representation of the polygon representing the area of interest.
#### **```verbose```:**
Verbosite of the _dhusget_ script provided by Copernicus. Set True for full verbosity, False for a silent execution.
#### **```processingmode```:**
Parameter for specifying the timeliness of the products:
- Set ```processingmode = 'NR'``` for Near Real-Time products.
- Set ```processingmode = 'NT'``` for Non-Time Critical products.
#### **```username``` & ```password```:**
For authentication, you can use _s5pguest_ as the username and the password **ONLY** if you are trying to download data products from **Sentinel-5P**.
If you want to download data from previous Sentinel missions, you should create an account at https://scihub.copernicus.eu/dhus/#/self-registration.


## License

Copyright © 2020. Banco Interamericano de Desarrollo ("BID"). Uso autorizado. [AM-331-A3](/LICENSE.md)

## Authors

SentinelDownloader was developed by:
- Jerónimo Luza (jeronimol at iadb.org)
- Santiago Inmediato (santiagoi at iadb.org)


## Acknowledgments / Reconocimientos

**Copyright © [2025]. Inter-American Development Bank ("IDB"). Authorized Use.**  
The procedures and results obtained based on the execution of this software are those programmed by the developers and do not necessarily reflect the views of the IDB, its Board of Executive Directors or the countries it represents.

**Copyright © [2025]. Banco Interamericano de Desarrollo ("BID"). Uso Autorizado.**  
Los procedimientos y resultados obtenidos con la ejecución de este software son los programados por los desarrolladores y no reflejan necesariamente las opiniones del BID, su Directorio Ejecutivo ni los países que representa.

### Support and Usage Documentation / Documentación de Soporte y Uso

**Copyright © [2025]. Inter-American Development Bank ("IDB").** The Support and Usage Documentation is licensed under the Creative Commons License CC-BY 4.0 license. The opinions expressed in the Support and Usage Documentation are those of its authors and do not necessarily reflect the opinions of the IDB, its Board of Executive Directors, or the countries it represents.

**Copyright © [2025]. Banco Interamericano de Desarrollo (BID).** La Documentación de Soporte y Uso está licenciada bajo la licencia Creative Commons CC-BY 4.0. Las opiniones expresadas en la Documentación de Soporte y Uso son las de sus autores y no reflejan necesariamente las opiniones del BID, su Directorio Ejecutivo ni los países que representa.
