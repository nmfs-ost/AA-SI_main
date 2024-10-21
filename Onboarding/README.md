# Onboarding Materials for Active Acoustics Strategic Initiative

# Background


# Data collection: Equipment
## EK80  
The EK80 is the latest in the Kongsberg line of scientific echosounders. All NOAA FSVs and ships that have scientific echosounders collect data using the EK80. "EK80" refers to the echosounder (hardware that generates an electrical signal that is transmitted to the acoustic transducer and receives an electrical signal (voltage) that is then digitized and sent to the acquisition software, also known as "EK80". The EK80 has several echosounders that can be used. The shipboard echosounder is called a Wide-Band Transceiver (WBT), and portable units are WBT-Tubes or WBATs (Wide-Band Autonomous Transceivers).  

## EK60  
The EK60 is the previous generation scientific echosounder. It was introduced in the late 1990s, but was installed on NOAA ships in the early 2000s. The majority of data collected by NOAA is from the EK60. The echosounder was called the General Purpose Transceiver (GPT) and the data acquisition software was called "ER60". The EK80 software can control both WBTs and GPTs. Which software, ER60 or EK80, recorded the data is important to distinguish because the digital format of the data are different depending on software version.  

## EK500
The EK500 was used from the 1980s (1970s?) until the early 2000s on NOAA ships. More on this...   

# Data collection: Formats
The EK500, EK60/ER60, and EK80 echosounders recorded data in binary format. The format is proprietary and was developed by Kongsberg. Kongsberg freely distributes the format for anyone with interest in the data to develop software to read the data. The format differs among data acquisition systems and software, so it is important that the user know the source of the data. As part of this AA-SI, we will be primarily working with data that have been converted from the Kongsberg-format data (e.g., ".raw" files) to netCDF4 format by [Echopype](https://echopype.readthedocs.io/en/stable/). We will be heavily invested in Echopype, so we will focus on the netCDF4 format.  
  
The netCDF4 acoustic data follow several conventions: [netCDF4](https://unidata.github.io/netcdf4-python/), [SONAR-netCDF4](https://github.com/ices-publications/SONAR-netCDF4), and [AcMeta](https://github.com/ices-publications/AcMeta).  
  
## netCDF4 - EK80
For now we start with .raw data that have been converted to netCDF4 format. This is done using a variation of the code:  
```
import echopype as ep
ed = open_raw(raw-format-filename, sonar_model='EK80')
ed.to_netcdf(save_path=output-filename)
```
In this case, we use "EK80" for the sonar_model because we used the EK80 to record the data. The output-filename will have a ".nc" extension.  

### We will use [pathlib](https://docs.python.org/3/library/pathlib.html) for our file paths. 

Open the newly created netCDF4 file(s):
```
import echopype as ep
import pathlib as Path
# list of file names
filenames = [Path(file1.nc), Path(file2.nc), ...]
# "ed" is short for "echo data"
edlist = []
for f in filenames:
    edlist.append(ep.open_converted(str(f)))
# combine the data files into one xarray data set
ed = ep.combine_echodata(edlist)
```
"ed" is the echo data object. To see the contents of the object, type  
```
ed
```
You will see the top-level headers for the data.  


# Data standardization
