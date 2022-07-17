## __Seasonality polar plots__
 
This is a package to create polar plots for displaying seasonal trends in time series data.
Requires
- matplotlib (3.5.1)
- numpy (1.19.2)
- pandas (1.3.5)
- seaborn (0.11.2)
- scipy (1.6.0)
### 1. Read data into SeasonData class:
~~~
from season_polar_plots import SeasonData
~~~
### SeasonData(data, year_start, year_end, t_res = 'daily') 
#
| Arguments  |   |
| ------ | ------ |
| data | pandas Series or single column DataFrame with datetime index |
| year_start | (int) start year of period to be analyzed |
| year_end | (int) end year of period to be analyzed |
| t_res | 'daily' or 'monthly': temporal resolution. Monthly values can be aggregated from daily values if 'monthly' is chosen (see sp_plot() and get_mgrid() function) |

### 2. Plot function:
### _self_.sp_plot(label, mode = 'all', rd_years = True, col = 'viridis_r', a = 1, psize = None, pmarker = None, nylabels = 10, off = 0, rlab_angle = 15, linreg = False, start_month = 1)
#
| Arguments  |   |
| ------ | ------ |
| label | label for time series variable |
| mode | 'all' to select all data points; daily resolution: 'min' or 'max' filter time series on annual extreme values; monthly resolution:  'sum', 'mean' / 'min', 'max' aggregate / filter data for each month |
| rd_years | as default, years are plotted in radius direction; rd_years=False plots variable in radius direction |
| col |  color gradient (default 'viridis_r') |
| a | transparency alpha (0-1) |
| psize | marker size for daily data points |
| pmarker | marker style  for daily data points|
| nylabels | number of (year) labels in radius direction |
| off | off-set from circle center |
| rlab_angle | angle of the radius axis labels |
| linreg | linreg=True plots linear regression (day in year ~ year) in polar projection (only for daily extreme values) |
| start_month | start month for linear regression |

__Returns__: Plot; if linreg=True prints R² and p-values for slope and intercept

#### Obtain annual extreme values from daily time series:
### _self_.get_ev( mode)
#
| Arguments  |   |
| ------ | ------ |
| mode | 'min' or 'max': filter time series on annual extreme values |

__Returns__: DataFrame (containing nr of day in year of extreme values, extreme values) 
#
#### Obtain aggregated / filtered monthly values:
### _self_.get_mgrid(mode)
#
| Arguments  |   |
| ------ | ------ |
| mode | 'all' if data is already in monthly resolution; 'sum', 'mean' / 'min', 'max' aggregate / filter data for each month |

__Returns__: DataFrame (containing monthly data) 

### 3. Von-Mises distribution (ML fit with scipy):
### _self_.von_mises(mode, plot = True, print_par = True, bins = 15, col_hist = 'b', col_vm ='r', off = 0.1, a = 1, rwidth = 0.8)
#
| Arguments  |   |
| ------ | ------ |
| mode | 'all' to use all data points, 'min' or 'max' to filter on extreme values |
| plot | if True plots the data as circular histogram and fitted von-Mises distribution |
| print_par | if True prints the fitted von-Mises parameters kappa and mu |
| bins | number of bins for histogram |
| col_hist | color of the histogram |
| col_vm | color of the fitted von Mises distribution |
| off | off-set from circle center |
| a | transparency alpha (0-1) |
| rwidth | relative width of histogram bins |

__Returns__: Plot; kappa, mu, mu_nday 