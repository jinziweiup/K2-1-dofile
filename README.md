cd C:\Users\pku\Desktop\AB
use A.dta,clear
tostring id hhid pid ,replace
save A1.dta,replace

use "HHS2016_HEALTH_K2_clean.dta",clear
rename _merge merge1
duplicates report hhidpid
rename hhidpid id
merge 1:1 id using A1.dta 
rename _merge merge_K2_A
save 1.dta,replace
/*用k2表和A表对*/

use B1B2.dta,replace
tostring id hhid pid ,replace
merge 1:1 id using 1.dta
rename _merge merge_B1B2_K2_A
save 2.dta,replace
/*用上面结果和B1B2对*/




result
merge 1:1 id using A1.dta 
(label _merge already defined)
Result                           # of obs.
----------------------------------------
not matched                        11,251
from master                        35  (_merge==1)
from using                     11,216  (_merge==2)
matched                             8,550  (_merge==3)
-----------------------------------------


merge 1:1 id using 1.dta
(note: variable id was str9, now str17 to accommodate using data's values)
Result                           # of obs.
-----------------------------------------
not matched                        12,405
from master                         0  (_merge==1)
from using                     12,405  (_merge==2)
matched                             7,396  (_merge==3)
---------------------------------
