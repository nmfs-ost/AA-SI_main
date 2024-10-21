# netCDF4 Acoustic Data Format
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

## netCDF4 - EK60


## netCDF4 - EK500


