# OHIE-HTE-Simulation

This is the code for "Heterogeneous effects of Medicaid coverage on cardiovascular risk factors: secondary analysis of randomized controlled trial (Inoue K, Athey S, Baicker K, and Tsugawa Y)" published in <i>BMJ 2024;386:e079377</i>.<br/>
https://www.bmj.com/content/386/bmj-2024-079377
 

In this repository, we include the code necessary to replicate the results from our paper and to test the code on simulated data. To use the code, the user should clone the repository into a directory on their local machine, and the scripts and notebooks can be run within that directory structure. The authors of the original studies analyzing the Oregon Health Insurance Experiment (OHIE) have made the data publicly available.  For users who have not obtained the OHIE data, we created a simulated dataset in order to demonstrate the code and its functionality. This code will run using only the data files provided in this repository. To replicate the manuscript results using the OHIE data, it is necessary to download the original data from either NBER or Harvard Dataverse and follow the instructions below.<br/>

 

<br/>

The repository has the following files and folders<br/>

- <b>OHIE-HTE-SimCodeResults.Rmd</b>: R code that generates the results reported in our paper. It includes flags that the user can set that specify which initial and intermediate data files are used in subsequent steps of the analysis.<br/>

- <b>outputAsPublished</b>: Includes the following two outputs.<br/>
    <ul>
        <li>
             OHIE-HTE-SimCodeResults.html: output created when the authors ran the R code on simulated data (the user can compare their results to this output) 
        </li>
        <li>
             OHIE-HTE-PublishedCodeResults.html: Output created when the authors ran the R code on real data (the user can compare their results to this output if they download OHIE data)   
        </li>
    </ul>

- <b>datGen</b>: Data generation of the simulated dataset<br/>

- <b>datImport</b>: Code to create the data for analysis from the original OHIE data provided in NBER or Harvard Dataverse<br/>

- <b>intdat</b>: intermediate datasets created when the user runs the R codes on the user's computers (users can save data in this folder)<br/>

- <b>intdatAsPublished</b>: intermediate datasets created when the paper authors ran the code (users should not save data in this folder)<br/>

- <b>output</b>: output files created when running the R codes in users' computer<br/>

 
<br/>
<b><em>A. Instructions to replicate results based on simulated data:</em></b><br/>

 

1. If desired, recreate the simulated data by running <b>datGen/DataGeneration.Rmd</b> which saves out "datGen/SIMdata_for_analysis.dta".  This is not necessary, as the repository includes the data file.<br/>

2. Run <b>OHIE-HTE-SimCodeResults.Rmd</b> with the default flags, which are set to read in the simulated data "datGen/SIMdata_for_analysis.dta" and write out "output/OHIE-HTE-SimCodeResults.html".<br/>

3. Because random forest imputation using different versions of missRanger may yield slightly different results, we have also provided intermediate files in the "intdatAsPublished" directory.  If you have difficulty replicating the precise results using the simulated data, change the flag <i>load_impdata=0</i> in <b>OHIE-HTE-SimCodeResults.Rmd</b> to <i>load_impdata=1</i>, which will cause the script to read in the intermediate data file using the missRanger result. <br/>

  
<br/>
<b><em>B. Instructions to download and clean the OHIE data:</em></b><br/>

 

1. Go to one of these websites, review the data use agreement, and follow the instructions to download data.

<b>NBER</b>: https://www.nber.org/programs-projects/projects-and-centers/oregon-health-insurance-experiment?page=1&perPage=50 <br/>

<b>Harvard Dataverse</b>: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/SJG1ED

<br/>

 

2. Add the following data to datImport/Data folder, and then run do file (<i>prepare_data_modified.do</i>) to obtain data for analysis.<br/>

<i>oregonhie_survey12m_vars.dta</i><br/>

<i>oregonhie_descriptive_vars.dta</i><br/>

<i>oregonhie_stateprograms_vars.dta</i><br/>

<i>oregonhie_inperson_vars.dta</i><br/>

<i>oregonhie_ed_vars.dta</i><br/>

 

This script will save "datGen/data_for_analysis.dta" <br/>

 
<br/>
<b><em>C. Instructions to replicate results based on real data:</em></b><br/>

1. Follow the instructions in section B above.<br/>

2. In OHIE-HTE-SimCodeResults.Rmd, to ensure the code reads in the real data, replace the flag <i>simulate_data=1</i> in <b>OHIE-HTE-SimCodeResults.Rmd</b> to <i>simulate_data=0</i>. <br/>

3. Follow the steps A1-A3 above. <br/>
 <br/>
- If imputation using a different version of missRanger yields different results for you, we will also provide the intermediate file (i.e., the dataset imputed using missRanger version 2.4.0) of the original OHIE dataset. The intermediate files can be placed in the <b>intdatAsPublished</b> and when flags are set appropriately, the code will read in the intermediate dataset. <br/>
 <br/>
- In addition, the grf software package that we use warns that results may vary across machines due to differences in rounding and representations of floating point numbers; in addition, results will differ with different number of cores.  Our analysis will report to the user if their machine has too few cores (less than 12) to precisely reproduce the results. <br/>
 <br/>
- If you have obtained permission from the original sources and would like to request the intermediate file or/and the forest predictions produced when the code was run to produce the published results, please contact the authors at <i>inoue.kosuke.2j@kyoto-u.ac.jp</i>.
