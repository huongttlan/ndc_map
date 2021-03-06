#### Mapping of U.S. Food and Drug Administration (FDA) National Drug Codes (NDC) to Anatomical Therapeutic Chemical (ATC) Level 4 classes
###### codename: ndc_map
  
This script reads a file called _NDC_MASTER_INFO.csv_ with the following columns:  
**"YEAR", "MONTH", "NDC"**  
and outputs a file called _ndc_atc_long_list.csv_ containing the following columns:  
**"YEAR", "MONTH", "NDC", "RXCUI", "ATC4"**  
as well as another file called atc_name.csv with the following columns:  
**"ATC4", "ATC4_NAME"**  

The script maps each NDC, according to the date it was used (year and month), to all its ATC-4 classes (if any is available) by querying the RxNav API at https://rxnav.nlm.nih.gov/. The algorithm uses parallelization and query caching to greatly improve efficiency. At my 8-cores desktop computer, I mapped 2.1 million YEAR-MONTH-NDC rows to 3.33 million YEAR-MONTH-NDC-RXCUI-ATC4 rows in 65 minutes.  
  
This work was presented as a poster at the 2017 Annual Symposium of AMIA (American Medical Informatics Association). If you are going to use this script, please take some time to understand the numbers contained in the poster (the PDF is in this repository), because they CAN affect data analysis done using the NDC-to-ATC map. For a deeper analysis and comparison of drug classification systems, we have also published a paper: https://mor.nlm.nih.gov/pubs/pdf/2016-dmmi-fk.pdf  
  
All contents of this repository are under an Attribution-ShareAlike-NonCommercial 4.0 International license. Please see details at http://creativecommons.org/licenses/by-nc-sa/4.0/.  
  
Please feel free to contact me about this work! Reading and reusing code can be made so much easier after a quick voice talk with the original author.  
  
**_If you do not know the R programming language or are unable to run the code yourself for any reason, and just need a NDC-to-ATC4 map for your project, check the FDA National Drug Code Directory ATC4 maps already available here in two versions: March, 2018 and March, 2019. Otherwise, if you can send me your list of NDCs, I can run the script for you, albeit with no guarantees/warranties whatsoever. Just contact me, you can find my email at https://directory.columbia.edu/people/uni?code=fk2374, or reach me via LinkedIn._**  
**--Fabrício Kury, formerly a postdoc at the U.S. National Library of Medicine**  
  
Search tags: thesaurus drug class map equivalence correspondance classification
  
#### Why do I need the year and month the NDC was used?  
One same NDC can be reused, i.e. represent different drugs at different points in time (https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfcfr/CFRSearch.cfm?fr=207.35, paragraph 4.ii). This regulation might be changed in 2017 (with tolerance period until 2019, see https://www.fda.gov/Drugs/GuidanceComplianceRegulatoryInformation/DrugRegistrationandListing/ucm2007058.htm), but old data will remain potentially ambiguous. If you do not have the year and month that each NDC was truly used (e.g. the date the drug was dispensed), the least wrong way to use this script might be to assign to all NDCs the year and month you are executing the script. This will attribute to each NDC its most recent ATC-4 class(es).

#### Can I get ATC-5? Or other drug classification systems?
It is possible to obtain ATC-5, but it requires a different path along the RxNorm resources and IDs; namely, one needs to map the RxNorm CUI of the medication to its ingredients, then request the ATC-5 of each one. It is also possible to request other drug/pharmaceutical classification systems besides ATC. These functionalities are possible but are not currently implemented in this script. If you want to implement them yourself, please refer to the RxNorm documentation for orientation: https://rxnav.nlm.nih.gov/  
