![OSP](https://user-images.githubusercontent.com/52009346/62771366-56c69f00-ba9d-11e9-9c86-a868bf3a1180.png)

## Index ##

* [Introduction](#introduction)
* [Getting started](#getting-started)
* [Tutorial](#tutorial)
* [Versioning](#versioning)
* [Authors](#authors)
* [History](#history)
* [License](#license)

## Introduction
Pwptemp is a small LGPL licensed library for easy calculation of the
temperature distribution along the well. Features are added as they
are needed; suggestions and contributions of all kinds are very welcome.

To catch up on the latest development and features, see the [changelog](CHANGELOG.md).

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Get pwptemp

* Users: Wheels for Python from [PyPI](https://pypi.python.org/pypi/pwptemp/) 
    * `pip install pwptemp`
* Developers: Source code from [github](https://github.com/pro-well-plan/pwptemp)
    * `git clone https://github.com/pro-well-plan/pwptemp`
    
## Tutorial

You can use the package by creating a new file and by following the instructions provided below.
   
### Basics   

1. Installing the package:
   > Option 1: Go to project interpreter settings and search pwptemp.
   
   > Option 2: Go to the terminal and type `pip install pwptemp`
   
2. Importing the dictionary and creating a new instance WellTemperature:
```
from pwptemp.Input import WellTemperature, temp_dict

tdata=temp_dict 
mw=WellTemperature(tdata)  
```

3. Defining wellpath:
```
from pwptemp.WellPath import wellpath

md,tvd,deltaz,zstep=wellpath(mw.mdt)  # Getting depth values
```

4. Calculating temperature distribution:
```
from pwptemp.Main import temp_time

#For circulation time = 5 hours
Tdsi,Ta,Tr,Tcsg,Tsr,Tfm=temp_time(5,mw,tvd,deltaz,zstep)
```

5. Plotting Temperature profile:
```
from pwptemp.Graph import plot_temp_profile

plot_temp_profile(Tdsi,Ta,Tr,Tcsg,Tfm,Tsr,mw.riser,md)
```

### Code Distribution

The code is compound different files as follows:

> **Wellpath.py** ▷ contains a function to define the MD, and TVD values from the wellpath.

> **Input.py** ▷ creates a class (WellTemperature) to have access to the parameters of the case.

> **InitCond.py** ▷ defines the initial and boundary conditions.

> **HeatCoefficients.py** ▷ contains a function to calculate the coefficients for the heat tranfer equations that will be used.

> **LinearSystem.py** ▷ contains a function to generate the entire temperature profile. 

> **Graph.py** ▷ contains a function to plot Tfm, Ta(bottom), Ta(outlet) vs time. And another function to plot the temperature profile.

> **Main.py** ▷ contains a function to determine the temperature profile at any time and another function to calculate for the stabilization time.

### Inputs

Around 43 data [inputs](inputs.md) (such as depths, diameters, temperatures, densities and operation parameters) are involved in pwptemp. However default values are provided in order to only change the parameters that the user wants to load.

### Outputs

Pwptemp allows users to count with heat data for different sections of a well and also to calculate the temperature values at certain circulation times (drilling operation).

```
Temperature of the fluid inside the Drill String (Tdsi)
Temperature of the Drill String Wall (Tds)
Temperature of the fluid inside the Annular (Ta)
Temperature of the Casing (Tcsg)
Temperature of the Riser (Tr)
Temperature of the Surrounding Space (Tsr)
Temperature of the Formation (Tfm)
```
![Diapositiva1](https://user-images.githubusercontent.com/52009346/62273419-d4efc980-b43d-11e9-974e-4cbbf086c0ff.JPG)

> Note 1: Above seabed, casing section is replaced with the riser and surrounding space would be sea water.

> Note 2: Beyond the 'undisturbed formation zone' the temperature keeps constant (Tfm).     

### Distribution Scheme

<img src="https://user-images.githubusercontent.com/52009346/62863045-fbe4b000-bd07-11e9-9bda-30330dc612d1.PNG" width="450" height="400"> <img src="https://user-images.githubusercontent.com/52009346/62856722-f4b4a680-bcf5-11e9-80ef-751e03b4dbc2.PNG" width="200" height="180">

## Contributing

Please read [CONTRIBUTING](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/pro-well-plan/pwptemp/tags). 

## Authors

* **Eirik Lyngvi** - *Initial work* - [elyngvi](https://github.com/elyngvi)
* **Juan Camilo Gonzalez Angarita** - *Initial work* - [jcamiloangarita](https://github.com/jcamiloangarita)
* **Muhammad Suleman** - *Initial work* - [msfazal](https://github.com/msfazal)


See also the list of [contributors](https://github.com/jcamiloangarita/WT/graphs/contributors) who participated in this project.

## History ##
Pwptemp was initially written and is maintained by [Pro Well plan
AS](http://www.prowellplan.com/) as a free, simple, easy-to-use way of getting
temperature data that can be tailored to our needs, and as contribution to the
free software community.

## License

This project is licensed under the GNU Lesser General Public License v3.0 - see the [LICENSE](LICENSE.md) file for details
