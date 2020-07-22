# Capstone-Project-Code
*** Create a SAS data set from a single SAS transport file;
 *** The SAS transport file(s) must be downloaded from the KAGGLE web site and 
     then unzipped before running this program;
 LIBNAME sasdata '/folders/myfolders/sasuser.v94';
 FILENAME in1 '/folders/myfolders/MIS445/netflix_titles.csv';
 proc xcopy in = in1 out = sasdata IMPORT;
 RUN;
 TITLE 'NETFLIX TITLES DATA';
          PROC IMPORT DATAFILE=REFFILE
          DBMS=CSV
          OUT=WORK.IMPORT1;
          GETNAMES=YES;
          RUN;
 
 
              data WORK.IMPORT1    ;
              %let _EFIERR_ = 0; /* set the ERROR detection macro variable */
              infile REFFILE delimiter = ',' MISSOVER DSD  firstobs=2 ;
                 informat show_id best32. ;
                informat type $7. ;
                informat title $50. ;
                informat director $33. ;
                informat cast $180. ;
                informat country $53. ;
                informat date_added anydtdtm40. ;
                informat release_year best32. ;
                informat rating $8. ;
                informat duration $8. ;
                informat listed_in $67. ;
                informat description $152. ;
                format show_id best12. ;
                format type $7. ;
                format title $50. ;
                format director $33. ;
                format cast $180. ;
                format country $53. ;
                format date_added datetime. ;
                format release_year best12. ;
                format rating $8. ;
                format duration $8. ;
                format listed_in $67. ;
                format description $152. ;
            input
                         show_id
                         type  $
                         title  $
                         director  $
                         cast  $
                         country  $
                         date_added
                         release_year
                         rating  $
                        duration  $
                         listed_in  $
                         description  $
             ;
             if _ERROR_ then call symputx('_EFIERR_',1);  /* set ERROR detection macro variable */
             run;
