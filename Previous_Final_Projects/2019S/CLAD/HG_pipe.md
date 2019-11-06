"""This file contains functions to obtain properties of the pipe
"""
```python
from aguaclara.core.units import unit_registry as u
import numpy as np
import pandas as pd
#load the HG_pipe_info from a csv file

import os.path
dir_path = os.path.dirname(__file__)
csv_path = os.path.join(dir_path, 'HG_pipe_crossing_data.csv')
with open(csv_path) as HGpipefile:
    HG_pipe_info = pd.read_csv(HGpipefile)

""""""
class HG_Pipe:


    def __init__(self, nd):
        self.nd= nd

    @property
    def od(self):
        index = (np.abs(np.array(HG_pipe_info['NDinch']) - self.nd.magnitude)).argmin()
        return HG_pipe_info.iloc[index, 2] * u.inch



@u.wraps(u.inch, u.inch, False)
def OD(ND):
    """Return a pipe's outer diameter according to its nominal diameter.

    """
    index = (np.abs(np.array(HG_pipe_info['NDinch']) - (ND))).argmin()
    return HG_pipe_info.iloc[index, 2]


@u.wraps(u.inch, u.inch, False)
def ID(ND):
    """Return the inner diameter for schedule 40 pipes.
    The ID info for these pipes is in the HG_pipe_info.
    """
    myindex = (np.abs(np.array(HG_pipe_info['NDinch']) - (ND))).argmin()
    return (HG_pipe_info.iloc[myindex, 3])


def thickness(ND):
    """Return the thickness for a pipe.
    wall thickness available is available in the HG_pipe_info.
    """

    myindex = (np.abs(np.array(HG_pipe_info['NDinch']) - (ND))).argmin()
    return (HG_pipe_info.iloc[myindex, 4])


def weight(ND):
    """Return an array of inner diameters with a given SDR.
    Weight (lb/ft) available in the HG_pipe_info.
    """
    myindex = (np.abs(np.array(HG_pipe_info['NDinch']) - (ND))).argmin()
    return (HG_pipe_info.iloc[myindex, 5])

```
