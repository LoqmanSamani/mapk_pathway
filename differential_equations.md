﻿


# Differential equation model (which defines only one state for each protein).
-------------------------------------------------------------------------------




                                                
# THE FIRST MODEL
-----------------
        ----------------------------------------------------------------------------------------------------------------------------------------------
        
             **REACTIONS**                **RATE EQUATIONS**                      **RATE OF CHANGE**
        ----------------------------------------------------------------------------------------------------------------------------------------------
        R1: EGF ->  Raf               r0  * EGF  
              
        R2: Raf ->  Mek               r1  * Raf                         dEGF/dt  = - r0 * EGF  
        
        R3: Mek ->  Raf               r_1 * Mek                         dRaf/dt  = (r0 * EGF) + (r_3 * Erk) + (r_1 * Mek) - (r3 * Raf) - (r1 * Raf)
        
        R4: Mek ->  Erk               r2  * Mek                         dmek/dt  = (r1 * Raf) + (r_2 * Erk) - (r_1 * Mek) - (r2 * Mek) 
        
        R5: Erk ->  Mek               r_2 * Erk                         dErk/dt  = (r3 * Raf) + (r2 * Mek) - (r_2 * Erk) - (r_3 * Erk) - (d * Erk)
        
        R6: Raf ->  Erk               r3  * Raf  
                
        R7: Erk ->  Raf               r_3 * Erk   
              
        R8: Erk ->  NaN               d   * Erk                


        -----------------------------------------
        ## The simplest way to describe the model






# differential equation models (which define an active (phosporilated) and an inactive (non-phosporilated) state for each protein)
-----------------------------------------------------------------------------------------------------------------------------------






# THE SECOND MODEL
----------------------
        -----------------------------------------------------------------------------------------------------------------------------------------------------------------------
        
             **REACTIONS**                **RATE EQUATIONS**                      **RATE OF CHANGE**
        -----------------------------------------------------------------------------------------------------------------------------------------------------------------------
        R1: EGF  + Raf   ->  pRaf        r0   * EGF  * Raf

        R2: pRaf + Mek   ->  pMek        r1   * pRaf * Mek          dEGF/dt  = - r0 * EGF * Raf 

        R3: pMek + pRaf  ->  Raf         r_1  * pMek * pRaf         dRaf/dt  = (r_1 * pMek * pRaf) + (r_3 * pErk * pRaf) - (r0 * EGF * Raf)

        R4: pMek + Erk   ->  pErk        r2   * pMek * Erk          dmek/dt  = (r_2 * pErk * pMek) - (r1 * pRaf * Mek)

        R5: pErk + pMek  ->  Mek         r_2  * pErk * pMek         dErk/dt  = (r4 * pErk)         - (r3 * pRaf * Erk)   - (r2 * pMek * Erk)

        R6: pRaf + Erk   ->  pErk        r3   * pRaf * Erk          dpRaf/dt = (r0 * EGF * Raf)    - (r_1 * pMek * pRaf) - (r3 * pRaf * Erk) - (r_3 * pErk * pRaf)

        R7: pErk + pRaf  ->  Raf         r_3  * pErk * pRaf         dpMek/dt = (r1 * pRaf * Mek)   - (r_1 * pMek * pRaf) - (r2 * pMek * Erk) - (r_2 * pErk * pMek)

        R8: pErk         ->  Erk         r4   * pErk                dpErk/dt = (r2 * pMek * Erk)   - (r_2 * pErk * pMek) + (r3 * pRaf * Erk) - (r_3 * pErk * pRaf) - (r4 * pErk)


        ----------------------------------------------------------------------------------------------------
        ## The logic of the model is wrong! but it can be the right model to reproduce the original article!







# THE THIRD MODEL
------------------
        ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        
             **REACTIONS**                      **RATE EQUATIONS**         **RATE OF CHANGE**
        ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

        R1: EGF  + Raf -> pRaf                  r0  * EGF  * Raf          dEGF/dt  = -r0 * EGF * Raf 
          
        R2: pRaf + Mek -> pMek                  r1  * pRaf * Mek          dRaf/dt  = -r0 * EGF * Raf

        R3: pMek       -> pRaf + Mek            r_1 * pMek * pRaf         dMek/dt  = (r_1 * pMek)      - (r1 * Mek * pRaf)

        R4: pMek + Erk -> pErk                  r2  * pMek * Erk          dErk/dt  = (r_2 * pErk)      + (r_3 * pErk)      - (r2 * Erk * pMek) - (r3 * Erk * pRaf)
 
        R5: pErk       -> pMek + Erk            r_2 * pErk * pMek         dpRaf/dt = (r0 * Egf * Raf)  + (r_1 * pMek)      + (r_3 * pErk)      - (r1 * Mek * pRaf) - (r3 * Erk * pRaf)

        R6: pRaf + Erk -> pErk                  r3  * pRaf * Erk          dpMek/dt = (r1 * Mek * pRaf) + (r_2 * pErk)      - (r_1 * pMek)      - (r2 * pMek * Erk)

        R7: pErk       -> pRaf + Erk            r_3 * pErk * pRaf         dpErk/dt = (r2 * Erk * pMek) + (r3 * Erk * pRaf) - (r_3 * pErk)
        

        ---------------------------------------------------------------------------------------------
        ## The logic of the model is correct! but it does not define a degradation equation for pErk,

           nor does it define an equation for the inverse of the R1 equation!





        
# THE FORTH MODEL
-----------------
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        
             **REACTIONS**                      **RATE EQUATIONS**         **RATE OF CHANGE**
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

        R1: EGF  + Raf -> pRaf                  r0  * EGF  * Raf          dEGF/dt  = (r_0 * pRaf) - (r0 * EGF * Raf) 
        
        R2 : pRaf      -> EGF + Raf             r_0 * pRaf
          
        R3: pRaf + Mek -> pMek                  r1  * pRaf * Mek          dRaf/dt  = (r_0 * pRaf) - (r0 * EGF * Raf)

        R4: pMek       -> pRaf + Mek            r_1 * pMek * pRaf         dMek/dt  = (r_1 * pMek)      - (r1 * Mek * pRaf)

        R5: pMek + Erk -> pErk                  r2  * pMek * Erk          dErk/dt  = (r_2 * pErk)      + (r_3 * pErk)      - (r2 * Erk * pMek) - (r3 * Erk * pRaf)
 
        R6: pErk       -> pMek + Erk            r_2 * pErk * pMek         dpRaf/dt = (r0 * Egf * Raf)  + (r_1 * pMek)      + (r_3 * pErk)      - (r1 * Mek * pRaf) - (r3 * Erk * pRaf)  - (r_0 * pRaf)

        R7: pRaf + Erk -> pErk                  r3  * pRaf * Erk          dpMek/dt = (r1 * Mek * pRaf) + (r_2 * pErk)      - (r_1 * pMek)      - (r2 * pMek * Erk)

        R8: pErk       -> pRaf + Erk            r_3 * pErk * pRaf         dpErk/dt = (r2 * Erk * pMek) + (r3 * Erk * pRaf) - (r_3 * pErk)
        
                          

       ---------------------------------------------------------------------------------------------------------- 

       ## This model adds an equation for the inverse of reaction R1.
          





# THE FIFTH MODEL
-----------------
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        
             **REACTIONS**                      **RATE EQUATIONS**         **RATE OF CHANGE**
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

        R1: EGF  + Raf -> pRaf                  r0  * EGF  * Raf          dEGF/dt  = (r_0 * pRaf) - (r0 * EGF * Raf) 
        
        R2 : pRaf      -> EGF + Raf             r_0 * pRaf
          
        R3: pRaf + Mek -> pMek                  r1  * pRaf * Mek          dRaf/dt  = (r_0 * pRaf) - (r0 * EGF * Raf)

        R4: pMek       -> pRaf + Mek            r_1 * pMek * pRaf         dMek/dt  = (r_1 * pMek)      - (r1 * Mek * pRaf)

        R5: pMek + Erk -> pErk                  r2  * pMek * Erk          dErk/dt  = (r_2 * pErk)      + (r_3 * pErk)      - (r2 * Erk * pMek) - (r3 * Erk * pRaf)
 
        R6: pErk       -> pMek + Erk            r_2 * pErk * pMek         dpRaf/dt = (r0 * Egf * Raf)  + (r_1 * pMek)      + (r_3 * pErk)      - (r1 * Mek * pRaf) - (r3 * Erk * pRaf)  - (r_0 * pRaf)

        R7: pRaf + Erk -> pErk                  r3  * pRaf * Erk          dpMek/dt = (r1 * Mek * pRaf) + (r_2 * pErk)      - (r_1 * pMek)      - (r2 * pMek * Erk)

        R8: pErk       -> pRaf + Erk            r_3 * pErk * pRaf         dpErk/dt = (r2 * Erk * pMek) + (r3 * Erk * pRaf) - (r_3 * pErk) - (d * pErk)
        
        R9: pErk       -> NaN (degradation)     d * pErk                  

       ---------------------------------------------------------------------------------------------------------- 

       ## This model is more complete than the others, it defines a degradation equation for pErk (why not Erk!).

          The only problem with this model is that it has an inverse equation for R1

         (since EGF is a stimulus, it may not be affected by the pathway proteins)!







-----------------------------------------------------------------------------------

Each model can be used for both  stimuli - NGF  and  EGF - as they stimulate 
the same signaling pathway. For each model, we prepared (for both stimuli)
10 different data sets  (.tsv and .yaml files),  each with  different parameter
ranges (they can be found in the  file_collection folder),  which can be used
to estimate the parameters with the pypesto package. Also, we have written
Python programs for all different sets of equations to estimate the unknown
parameters using a different method, They can be found in the params_estimation
folder.

Of course, the model can be  extended in several ways (e.g., by defining
degradation equations for each protein or defining the receptor tyrosine
kinases (TrkA) and the  epidermal  growth  factor receptor (EGFR) by two
different stimuli,  NGF and EGF,  respectively),  but we think that this
is not necessary for our study and is beyond the scope of our work!

------------------------------------------------------------------

Loghman Samani 

30.September.2023

