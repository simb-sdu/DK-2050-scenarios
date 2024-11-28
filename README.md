# DK2050 scenarios


Description
-----------

Implements danish scenarios of electricity and residential heat. Creates market for heating techologies, as well as average market for residential energy use. This is useful for prospective LCA of Danish buildings' energy use. A marketspecific for tiny houses is also created, i.e. not having access to district heat, geothermal ground heat, etc.

Sourced from publication
------------------------

Energy scenarios towards 2020, 2035, and 2050\
Danish Energy Agency\
https://ens.dk/sites/ens.dk/files/Basisfremskrivning/energiscenarier_-_analyse_2014_web.pdf/



Ecoinvent database compatibility
--------------------------------

ecoinvent 3.9.1 cut-off

IAM scenario compatibility
---------------------------
Following REMIND scenarioas are currently supported. This can fairly simply be extended\
SSP1-Base\
SSP2-Base\
SSP5-Base\
SSP1-PkBudg500\
SSP2-PkBudg500\
SSP5-PkBudg500\

What does this do?
------------------
Implements future DK scenarios for prodution of electricity and residential heat. Includes modifying ecoinvent datasets to reflect fuel types, efficiency, etc.

How to use it?
--------------

```python

import bw2data as bw
from premise import *
from datapackage import Package
    
fp = "/home/simb/PycharmProjects/DK-2050-scenarios/datapackage.json"
#fp = r"https://raw.githubusercontent.com/premise-community-scenarios/energy-perspective-2050-switzerland/main/datapackage.json"
ep2050 = Package(fp)
ep2050.errors #test for errors in datapackage
    
bw.projects.set_current("your_bw_project")
    
ndb = NewDatabase(
        scenarios = [
            {"model":"remind", "pathway":"SSP1-Base", "year":2035,},
            {"model":"remind", "pathway":"SSP1-PkBudg500", "year":2035,},
            {"model":"remind", "pathway":"SSP2-Base", "year":2035,},
            {"model":"remind", "pathway":"SSP2-PkBudg500", "year":2035,},
            {"model":"remind", "pathway":"SSP5-Base", "year":2035,},
            {"model":"remind", "pathway":"SSP5-PkBudg500", "year":2035,},
            {"model":"remind", "pathway":"SSP1-Base", "year":2050,},
            {"model":"remind", "pathway":"SSP1-PkBudg500", "year":2050,},
            {"model":"remind", "pathway":"SSP2-Base", "year":2050,},
            {"model":"remind", "pathway":"SSP2-PkBudg500", "year":2050,},
            {"model":"remind", "pathway":"SSP5-Base", "year":2050,},
            {"model":"remind", "pathway":"SSP5-PkBudg500", "year":2050,}
        ],        
        source_db="cutoff391",
        source_version="3.9.1",
        key='xxxxx,
        external_scenarios=[
            ep2050, # <-- list datapackages here
        ]
    )    
ndb.update_external_scenario()
```

