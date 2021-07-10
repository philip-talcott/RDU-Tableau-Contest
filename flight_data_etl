"""
Created on Tue Oct  4 21:10:48 2020

@author: ptalcott

"""

#Note: Before running, you should download the source files from the following link onto your computer: https://data.world/tylerudite/airports-airlines-and-routes

import pandas as pd
from datetime import datetime as dt

now = (dt.now())
datetime = now.strftime("%m-%d-%Y")

#import flight data files
routes = pd.read_csv(filepath_or_buffer = 'C:\\Users\\ptalcott\\Downloads\\routes.csv', sep = ',')
airlines = pd.read_csv(filepath_or_buffer = 'C:\\Users\\ptalcott\\Downloads\\airlines.csv', sep = ',')
airports = pd.read_csv(filepath_or_buffer = 'C:\\Users\\ptalcott\\Downloads\\airports.csv', sep = ',')
airplanes = pd.read_csv(filepath_or_buffer = 'C:\\Users\\ptalcott\\Downloads\\airplanes.csv', sep = ',')

routes['Airline ID'] = routes['Airline ID'].astype(str)
airlines['Airline ID'] = airlines['Airline ID'].astype(str)
airlines = airlines.rename(columns={'Name': 'Airline Name'})

#begin merging flight files together
df_merge1 = pd.merge(routes, airlines, how='left', on=None, left_on='Airline ID', right_on='Airline ID',
         left_index=False, right_index=False, sort=True,
         suffixes=('', ''),
         copy=True, indicator=False,
         validate=None)

airplanes = airplanes.rename(columns={'Name': 'Plane Name'})

df_merge2 = pd.merge(df_merge1, airplanes, how='left', on=None, left_on='Equipment', right_on='Plane Name',
         left_index=False, right_index=False, sort=True,
         suffixes=('', ''),
         copy=True, indicator=False,
         validate=None)

airports['Airport ID'] = airports['Airport ID'].astype(str)
airports = airports.rename(columns={'Name': 'Destination Name'})

df_merge3 = pd.merge(df_merge2, airports, how='left', on=None, left_on='Destination airport ID', right_on='Airport ID',
         left_index=False, right_index=False, sort=True,
         suffixes=('', '.destination_airports'),
         copy=True, indicator=False,
         validate=None)

airports = airports.rename(columns={'Destination Name': 'Departing Airport Name'})

df_merge4 = pd.merge(df_merge3, airports, how='left', on=None, left_on='Source airport ID', right_on='Airport ID',
         left_index=False, right_index=False, sort=True,
         suffixes=('', '.source_airports'),
         copy=True, indicator=False,
         validate=None)

#Save data to downloads folder with today's date
df_merge4.to_csv('flight data '+datetime+'.csv', index=False)

del df_merge1
del df_merge2
del df_merge3

