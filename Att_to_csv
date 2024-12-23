import os
import re
import glob
import arcpy
import pandas as pd
from arcpy.sa import *

at_table = []
fields = []
aliases = []
f_list = []

gdb_path = r" "  #provide path where all the files are located
out_path = r" " #provide path of the output locaiton

os.chdir(gdb_path)

f_list = arcpy.ListFeatureClasses()

total = (len(f_list))

i = 1

for pane in f_list:
  
  fname = os.path.basename(pane)
  
  for field in arcpy.ListFields(fname):
      fields.append(field.name)
      aliases.append(field.aliasName)
  
  with arcpy.da.SearchCursor(fname, fields) as cursor:
      for row in cursor:
          at_table.append(row)
  df = pd.DataFrame(at_table, columns=aliases)
  
  os.chdir(out_path)

  df.to_csv('{}.csv'.format(fname))
  
  df = pd.DataFrame()
  
  at_table = []
  fields = []
  aliases = []
  
  os.chdir(gdb_path)
  
  t_percent = (i*100)/total
  
  print (f"{t_percent:.2f}")
  i = i + 1
