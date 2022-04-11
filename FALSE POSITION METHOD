# -*- coding: utf-8 -*-
"""
Created on Mon Mar 28 23:38:23 2022

@author: RIFA TABASSUM MIM
"""

import math
import numpy as np
import xlwt
from xlwt import Workbook


xl=np.float(input ('Enter 1st initial value: '))   #1st input
print(xl)
xu=float(input ('Enter 2nd initial value: '))   #2nd input

#computing function values corresponding to initial values

fxl=(667.38/xl)*(1-math.exp(-0.146843*xl))-40
fxu=(667.38/xu)*(1-math.exp(-0.146843*xu))-40

#checking initial input values
if fxl*fxu>0:
        print('Wrong initial input')
#if the initial input is correct        
elif fxl*fxu<0:
    #taking input
    err=float(input('Enter desired percentage relative error: '))
    ite=int(input('Enter number of iterations: '))
    #initialization
    x_l=np.zeros([ite])
    x_u=np.zeros([ite])
    x_c=np.zeros([ite])
    
    f_xl=np.zeros([ite])
    f_xu=np.zeros([ite])
    f_xc=np.zeros([ite])
    
    rel_err=np.zeros([ite])
    itern=np.zeros([ite])
    #storing initial computed values into array
    x_l[0]=xl
    x_u[0]=xu
    
    f_xl[0]=fxl
    f_xu[0]=fxu 
    #begin iteration   
    for i in range(ite):
        #storing the values of iteration
        itern[i]=i+1
        #False position method formula
        
        
        f_xl[i]=(667.38/x_l[i])*(1-math.exp(-0.146843*x_l[i]))-40
        f_xu[i]=(667.38/x_u[i])*(1-math.exp(-0.146843*x_u[i]))-40
        
        
        
        x_c[i]= x_u[i]-(f_xu[i]*(x_l[i]-x_u[i]))/(f_xl[i]-f_xu[i])
        
        f_xc[i]=(667.38/x_c[i])*(1-math.exp(-0.146843*x_c[i]))-40
        
        #calculating error    
        if i>0:
            rel_err[i]=((x_c[i]-x_c[i-1])/x_c[i])*100
        #terminate if error criteria meets
        if all ([i>0, abs(rel_err[i])<err]):
            break 
        elif f_xc[i]==0:
            break
   
        if i==ite-1:
            break
        #replacement of the new estimate
        if all ([f_xc[i]>0, f_xl[i]>0]):
            x_l[i+1]=x_c[i]
            x_u[i+1]=x_u[i]
        elif all ([f_xc[i]>0, f_xu[i]>0]):
            x_u[i+1]=x_c[i]
            x_l[i+1]=x_l[i]
        elif all ([f_xc[i]<0, f_xl[i]<0]):
            x_l[i+1]=x_c[i]
            x_u[i+1]=x_u[i]
        elif all ([f_xc[i]<0, f_xu[i]<0]):
            x_u[i+1]=x_c[i]
            x_l[i+1]=x_l[i]
#Writing the results on an excel sheet    
    #Workbook is created
    wb = Workbook()
      
    # add_sheet is used to create sheet.
    sheet2 = wb.add_sheet('Sheet 2')
    num_of_iter=i
    
    #writing on excel
    sheet2.write(0,0,'Number of iteration')
    sheet2.write(0,1,'x_l')
    sheet2.write(0,2,'x_u')
    sheet2.write(0,3,'f(x_l)')
    sheet2.write(0,4,'f(x_u)')
    sheet2.write(0,5,'x_c')
    sheet2.write(0,6,'f(x_c)')
    sheet2.write(0,7,'Relative error')
    
    #writing values on excel    
    for n in range(num_of_iter+1):
        
        sheet2.write(n+1,0,itern[n])
        sheet2.write(n+1,1,x_l[n])
        sheet2.write(n+1,2,x_u[n])
        sheet2.write(n+1,3,f_xl[n])
        sheet2.write(n+1,4,f_xu[n])
        sheet2.write(n+1,5,x_c[n])
        sheet2.write(n+1,6,f_xc[n])
        sheet2.write(n+1,7,rel_err[n])
    
    sheet2.write(n+4,2,'The')
    sheet2.write(n+4,3,'root')
    sheet2.write(n+4,4,'is')
    sheet2.write(n+4,5,x_c[i])
    
    #save the excel file
    wb.save('false position.xls')
