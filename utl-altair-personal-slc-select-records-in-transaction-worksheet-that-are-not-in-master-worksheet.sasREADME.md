# utl-altair-personal-slc-select-records-in-transaction-worksheet-that-are-not-in-master-worksheet
RE: Altair personal slc select records in transaction worksheet that are not in master worksheet
%let pgm=utl-altair-personal-slc-select-records-in-transaction-worksheet-that-are-not-in-master-worksheet;

%stop_submission;

RE: Altair personal slc select records in transaction worksheet that are not in master worksheet

Too Long to Post to Listserv, see github

github
https://github.com/rogerjdeangelis/utl-altair-personal-slc-select-records-in-transaction-worksheet-that-are-not-in-master-worksheet

The trans worksheet is unique on amount, if there are multiples, -229 amounts in the master, WITH  DIFFERENT DATES,
YOU NEED MULTIPLE -229S IN THE RECOCILLIATION TO PESERVE ALL THE DATES IN THE MASTER.

SOLUTIONS

   1  left join with preserving date information in master
   2  left join without duplicates (keep only the maximum date in the master.)


community.altair
https://community.altair.com/discussion/4952

/*               _     _
 _ __  _ __ ___ | |__ | | ___ _ __ ___
| `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
| |_) | | | (_) | |_) | |  __/ | | | | |
| .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
|_|
*/

---------------------------------------------------------   ------------------------------------
                     INPUTS                                            OUTPUT
---------------------------------------------------------   ------------------------------------

MASTER                        TRANS                         RECONCILE

d:/xls/date.xlsx              d:/xls/date_2.xlsx            d:/xls/date.xlsx (added sheet)

-------------------------+    -------------------------+    -------------------------+
| A1| fx    |  NAME      |    | A1| fx    |POSTED_DATE |    | A1| fx       |JE_DATE  |
-------------------------+    -------------------------+    -----------------------------------+
[_] |    A     |    B    |    [_] |    A     |    B    |    [_] |    A     |    B    |    C    |
-------------------------|    -------------------------|    -----------------------------------|
 1  | JE_DATE  |TRANS_AMT|     1  | POSTED   | TRAN    |     1  | JE_DATE  |TRANS_AMT| STATUS  |
 -- |----------+---------|     1  | DATE     | AMOUNT  |     -- |----------+---------+---------|
 2  |  03JUN2021 -2843.75|     -- |----------+---------|     2  |  03JUN2021 -2843.75|         |
 -- |----------+---------|     2  | 06/09/2021  -350   |     -- |----------+---------+---------|
 3  |  01JUN2021 -2310.13|     -- |----------+---------|     3  |  01JUN2021 -2310.13|         |
 -- |----------+---------|     3  | 06/23/2021  -312.56|     -- |----------+---------+---------|
 4  |  07JUN2021 -726.21 |     -- |----------+---------|     4  |  07JUN2021 -726.21 |         |
 -- |----------+---------|     4  | 06/25/2021  -229   |     -- |----------+---------+---------|
 5  |  11JUN2021 -350    |     -- |----------+---------|     5  |  11JUN2021 -350    |In Trans |
 -- |----------+---------|     5  | 06/23/2021  -100   |     -- |----------+---------+---------|
 6  |  24JUN2021 -312.56 |     -- |----------+---------|     6  |  24JUN2021 -312.56 |In Trans |
 -- |----------+---------|     6  | 06/22/2021  -20    |     -- |----------+---------+---------|
 7  |  27JUN2021 -229    |     -- |----------+---------|     7  |  27JUN2021 -229    |In Trans | NOTE
 -- |----------+---------|     7  | 06/29/2021  -14.68 |     -- |----------+---------+---------| DIFFERENT
 8  |  27JUN2021 -229    |     -- |----------+---------|     8  |  27JUN2021 -229    |In Trans | MASTER DATES
 -- |----------+---------|     8  | 06/22/2021  -0.26  |     -- |----------+---------+---------| PRESERVE MASTER DATES
 9  |  30JUN2021 -229    |     -- |----------+---------|     9  |  30JUN2021 -229    |In Trans |
 -- |----------+---------|     9  | 06/21/2021  98     |     -- |----------+---------+---------|
10  |  25JUN2021 -100    |     -- |----------+---------|    10  |  25JUN2021 -100    |In Trans |
 -- |----------+---------|    10  | 06/10/2021  210.76 |     -- |----------+---------+---------|
11  |  24JUN2021 -20     |     -- |----------+---------|    11  |  24JUN2021 -20     |In Trans |
 -- |----------+---------|    11  | 06/22/2021  243.12 |     -- |----------+---------+---------|
12  |  30JUN2021 -14.68  |     -- |----------+---------|    12  |  30JUN2021 -14.68  |In Trans |
 -- |----------+---------|    12  | 06/29/2021  384.62 |     -- |----------+---------+---------|
13  |  21JUN2021 -0.26   |     -- |----------+---------|    13  |  21JUN2021 -0.26   |In Trans |
 -- |----------+---------|    13  | 06/23/2021  746.36 |     -- |----------+---------+---------|
14  |  22JUN2021 98      |     -- |----------+---------|    14  |  22JUN2021 98      |In Trans |
 -- |----------+---------|    14  | 06/04/2021  765.7  |     -- |----------+---------+---------|
15  |  11JUN2021 210.76  |     -- |----------+---------|    15  |  11JUN2021 210.76  |In Trans |
 -- |----------+---------|    15  | 06/30/2021  1027.47|     -- |----------+---------+---------|
16  |  24JUN2021 243.12  |     -- |----------+---------|    16  |  24JUN2021 243.12  |In Trans |
 -- |----------+---------|    16  | 06/30/2021  1000.21|     -- |----------+---------+---------|
17  |  30JUN2021 384.62  |     -- |----------+---------|    17  |  30JUN2021 384.62  |In Trans |
 -- |----------+---------|    [SHEET1]                       -- |----------+---------+---------|
18  |  23JUN2021 746.36  |                                  18  |  23JUN2021 746.36  |In Trans |
 -- |----------+---------|                                   -- |----------+---------+---------|
19  |  06JUN2021 765.7   |                                  19  |  06JUN2021 765.7   |In Trans |
 -- |----------+---------|                                   -- |----------+---------+---------|
20  |  18JUN2021 834.92  |                                  20  |  18JUN2021 834.92  |         |
 -- |----------+---------|                                   -- |----------+---------+---------|
21  |  28JUN2021 1027.47 |                                  21  |  28JUN2021 1027.47 |In Trans |
 -- |----------+---------|                                   -- |----------+---------+---------|
22  |  03JUN2021 2843.75 |                                  22  |  03JUN2021 2843.75 |         |
 -- |----------+---------|                                   -- |----------+---------+---------|
[SHEET1]                                                    [RECONCILE]


/*   _       __ _       _       _         _                        _       _
/ | | | ___ / _| |_    (_) ___ (_)_ __   | | _____  ___ _ __    __| | __ _| |_ ___  ___
| | | |/ _ \ |_| __|   | |/ _ \| | `_ \  | |/ / _ \/ _ \ `_ \  / _` |/ _` | __/ _ \/ __|
| | | |  __/  _| |_    | | (_) | | | | | |   <  __/  __/ |_) || (_| | (_| | ||  __/\__ \
|_| |_|\___|_|  \__|  _/ |\___/|_|_| |_| |_|\_\___|\___| .__/  \__,_|\__,_|\__\___||___/
                     |__/                              |_|
*/

/*---- only needed it you rerun                ----*/
/*---- sas and the slc cannot drop a worksheet ----*/
/*---- use r or python to drop sheet           ----*/
options set=RHOME "D:\d451";
proc r;
submit;
library(openxlsx)
wb <- loadWorkbook(file = 'd:/xls/data.xlsx')
removeWorksheet(wb,"reconcile")
saveWorkbook(wb, 'd:/xls/data.xlsx', overwrite = TRUE)
endsubmit;
run;quit;

libname  master excel "d:/xls/data.xlsx";
libname  trans excel "d:/xls/data-2.xlsx";

proc sql;
  create
     table master.reconcile as
  select
     master.je_date
    ,master.trans_amt
    ,trans.tran_amount
    ,case
       when (missing(trans.tran_amount)) then ''
       else 'In Trans'
     end as status
  from
     master.'sheet1$'n as master left join trans.'sheet1$'n as trans
  on
    master.trans_amt = trans.tran_amount
;quit;

libname  master clear;
libname  trans clear;

/*           _               _
  ___  _   _| |_ _ __  _   _| |_
 / _ \| | | | __| `_ \| | | | __|
| (_) | |_| | |_| |_) | |_| | |_
 \___/ \__,_|\__| .__/ \__,_|\__|
                |_|
*/

d:/xls/date.xlsx (added sheet)

-------------------------+
| A1| fx       |JE_DATE  |
-----------------------------------+
[_] |    A     |    B    |    C    |
-----------------------------------|
 1  | JE_DATE  |TRANS_AMT| STATUS  |
 -- |----------+---------+---------|
 2  |  03JUN2021 -2843.75|         |
 -- |----------+---------+---------|
 3  |  01JUN2021 -2310.13|         |
 -- |----------+---------+---------|
 4  |  07JUN2021 -726.21 |         |
 -- |----------+---------+---------|
 5  |  11JUN2021 -350    |In Trans |
 -- |----------+---------+---------|
 6  |  24JUN2021 -312.56 |In Trans |
 -- |----------+---------+---------|
 7  |  27JUN2021 -229    |In Trans | NOTE
 -- |----------+---------+---------| DIFFERENT
 8  |  27JUN2021 -229    |In Trans | MASTER DATES
 -- |----------+---------+---------|
 9  |  30JUN2021 -229    |In Trans |
 -- |----------+---------+---------|
10  |  25JUN2021 -100    |In Trans |
 -- |----------+---------+---------|
11  |  24JUN2021 -20     |In Trans |
 -- |----------+---------+---------|
12  |  30JUN2021 -14.68  |In Trans |
 -- |----------+---------+---------|
13  |  21JUN2021 -0.26   |In Trans |
 -- |----------+---------+---------|
14  |  22JUN2021 98      |In Trans |
 -- |----------+---------+---------|
15  |  11JUN2021 210.76  |In Trans |
 -- |----------+---------+---------|
16  |  24JUN2021 243.12  |In Trans |
 -- |----------+---------+---------|
17  |  30JUN2021 384.62  |In Trans |
 -- |----------+---------+---------|
18  |  23JUN2021 746.36  |In Trans |
 -- |----------+---------+---------|
19  |  06JUN2021 765.7   |In Trans |
 -- |----------+---------+---------|
20  |  18JUN2021 834.92  |         |
 -- |----------+---------+---------|
21  |  28JUN2021 1027.47 |In Trans |
 -- |----------+---------+---------|
22  |  03JUN2021 2843.75 |         |
 -- |----------+---------+---------|
[RECONCILE]

/*
| | ___   __ _
| |/ _ \ / _` |
| | (_) | (_| |
|_|\___/ \__, |
         |___/
*/

8439      ODS _ALL_ CLOSE;
8440      ODS LISTING;
8441      FILENAME WBGSF 'd:\wpswrk\_TD9616/listing_images';
8442      OPTIONS DEVICE=GIF;
8443      GOPTIONS GSFNAME=WBGSF;
8444
8445
8446      /*---- only needed it you rerun                ----*/
8447      /*---- sas and the slc cannot drop a worksheet ----*/
8448      /*---- use r or python to drop sheet           ----*/
8449      options set=RHOME "D:\d451";
8450      proc r;
8451      submit;
8452      library(openxlsx)
8453      wb <- loadWorkbook(file = 'd:/xls/data.xlsx')
8454      removeWorksheet(wb,"reconcile")
8455      saveWorkbook(wb, 'd:/xls/data.xlsx', overwrite = TRUE)
8456      endsubmit;
NOTE: Using R version 4.5.1 (2025-06-13 ucrt) from d:\r451

NOTE: Submitting statements to R:

> library(openxlsx)
> wb <- loadWorkbook(file = 'd:/xls/data.xlsx')
> removeWorksheet(wb,"reconcile")

NOTE: Processing of R statements complete

> saveWorkbook(wb, 'd:/xls/data.xlsx', overwrite = TRUE)
8457      run;quit;
NOTE: Procedure r step took :
      real time : 1.032
      cpu time  : 0.000


8458
8459      libname  master excel "d:/xls/data.xlsx";
NOTE: Library master assigned as follows:
      Engine:        OLEDB
      Physical Name: d:/xls/data.xlsx

8460      libname  trans excel "d:/xls/data-2.xlsx";
NOTE: Library trans assigned as follows:
      Engine:        OLEDB
      Physical Name: d:/xls/data-2.xlsx

8461
8462      proc sql;
8463        create
8464           table master.reconcile as
8465        select
8466           master.je_date
8467          ,master.trans_amt
8468          ,trans.tran_amount
8469          ,case
8470             when (missing(trans.tran_amount)) then ''
8471             else 'In Trans'
8472           end as status
8473        from
8474           master.'sheet1$'n as master left join trans.'sheet1$'n as trans
8475        on
8476          master.trans_amt = trans.tran_amount
8477      ;quit;
NOTE: Data set "MASTER.reconcile" has an unknown number of observation(s) and 4 variable(s)
NOTE: Procedure sql step took :
      real time : 0.564
      cpu time  : 0.359


NOTE: Libref MASTER has been deassigned.
8478
8479      libname  master clear;
NOTE: Libref TRANS has been deassigned.
8480      libname  trans clear;
8481
8482      quit; run;
8483      ODS _ALL_ CLOSE;
8484      FILENAME WBGSF CLEAR;


/*___    _       __ _       _       _         _                 _
|___ \  | | ___ / _| |_    (_) ___ (_)_ __   | |__   __ ___   _(_)_ __   __ _
  __) | | |/ _ \ |_| __|   | |/ _ \| | `_ \  | `_ \ / _` \ \ / / | `_ \ / _` |
 / __/  | |  __/  _| |_    | | (_) | | | | | | | | | (_| |\ V /| | | | | (_| |
|_____| |_|\___|_|  \__|  _/ |\___/|_|_| |_| |_| |_|\__,_| \_/ |_|_| |_|\__, |
                         |__/                                           |___/
                            _       _
 _ __ ___   __ ___  __   __| | __ _| |_ ___  ___
| `_ ` _ \ / _` \ \/ /  / _` |/ _` | __/ _ \/ __|
| | | | | | (_| |>  <  | (_| | (_| | ||  __/\__ \
|_| |_| |_|\__,_/_/\_\  \__,_|\__,_|\__\___||___/

*/

libname  master excel "d:/xls/data.xlsx";
libname  trans excel "d:/xls/data-2.xlsx";

proc sql;
  create
     table reconcileunq as
  select
     master.je_date
    ,master.trans_amt
    ,trans.posted_date
    ,trans.tran_amount
    ,case
       when (missing(trans.tran_amount)) then 'Not in Trans'
       else 'Exists in Trans'
     end as status
  from
     master.'sheet1$'n as master left join trans.'sheet1$'n as trans
  on
    master.trans_amt = trans.tran_amount
  group
    by trans_amt
  having
    master.je_date = max(master.je_date)
;quit;

libname  master clear;
libname  trans clear;

proc print data=reconcileunq width=min;
run;quit;


SLC TABLE WORK.RECONCILEUNQ

Altair SLC

Obs      JE_DATE      TRANS_AMT    POSTED_DATE    TRAN_AMOUNT        STATUS

  1    03-JUN-2021     -2843.75              .          .        Not in Trans
  2    01-JUN-2021     -2310.13              .          .        Not in Trans
  3    07-JUN-2021      -726.21              .          .        Not in Trans
  4    11-JUN-2021      -350.00    09-JUN-2021      -350.00      Exists in Trans
  5    24-JUN-2021      -312.56    23-JUN-2021      -312.56      Exists in Trans
  6    30-JUN-2021      -229.00    25-JUN-2021      -229.00      Exists in Trans
  7    25-JUN-2021      -100.00    23-JUN-2021      -100.00      Exists in Trans
  8    24-JUN-2021       -20.00    22-JUN-2021       -20.00      Exists in Trans
  9    30-JUN-2021       -14.68    29-JUN-2021       -14.68      Exists in Trans
 10    21-JUN-2021        -0.26    22-JUN-2021        -0.26      Exists in Trans
 11    22-JUN-2021        98.00    21-JUN-2021        98.00      Exists in Trans
 12    11-JUN-2021       210.76    10-JUN-2021       210.76      Exists in Trans
 13    24-JUN-2021       243.12    22-JUN-2021       243.12      Exists in Trans
 14    30-JUN-2021       384.62    29-JUN-2021       384.62      Exists in Trans
 15    23-JUN-2021       746.36    23-JUN-2021       746.36      Exists in Trans
 16    06-JUN-2021       765.70    04-JUN-2021       765.70      Exists in Trans
 17    18-JUN-2021       834.92              .          .        Not in Trans
 18    28-JUN-2021      1027.47    30-JUN-2021      1027.47      Exists in Trans
 19    03-JUN-2021      2843.75              .          .        Not in Trans

/*
| | ___   __ _
| |/ _ \ / _` |
| | (_) | (_| |
|_|\___/ \__, |
         |___/
*/

8485      ODS _ALL_ CLOSE;
8486      ODS LISTING;
8487      FILENAME WBGSF 'd:\wpswrk\_TD9616/listing_images';
8488      OPTIONS DEVICE=GIF;
8489      GOPTIONS GSFNAME=WBGSF;
8490
8491      libname  master excel "d:/xls/data.xlsx";
NOTE: Library master assigned as follows:
      Engine:        OLEDB
      Physical Name: d:/xls/data.xlsx

8492      libname  trans excel "d:/xls/data-2.xlsx";
NOTE: Library trans assigned as follows:
      Engine:        OLEDB
      Physical Name: d:/xls/data-2.xlsx

8493
8494      proc sql;
8495        create
8496           table reconcileunq as
8497        select
8498           master.je_date
8499          ,master.trans_amt
8500          ,trans.posted_date
8501          ,trans.tran_amount
8502          ,case
8503             when (missing(trans.tran_amount)) then 'Not in Trans'
8504             else 'Exists in Trans'
8505           end as status
8506        from
8507           master.'sheet1$'n as master left join trans.'sheet1$'n as trans
8508        on
8509          master.trans_amt = trans.tran_amount
8510        group
8511          by trans_amt
8512        having
8513          master.je_date = max(master.je_date)
8514      ;quit;
NOTE: Summary results are required to be remerged with the original data
NOTE: Data set "WORK.reconcileunq" has 19 observation(s) and 5 variable(s)
NOTE: Procedure sql step took :
      real time : 0.632
      cpu time  : 0.406


NOTE: Libref MASTER has been deassigned.
8515
8516      libname  master clear;
NOTE: Libref TRANS has been deassigned.
8517      libname  trans clear;
8518
8519      proc print data=reconcileunq width=min;
8520      run;quit;
NOTE: 19 observations were read from "WORK.reconcileunq"
NOTE: Procedure print step took :
      real time : 0.032
      cpu time  : 0.000


8521
8522      quit; run;
8523      ODS _ALL_ CLOSE;
8524      FILENAME WBGSF CLEAR;

/*              _
  ___ _ __   __| |
 / _ \ `_ \ / _` |
|  __/ | | | (_| |
 \___|_| |_|\__,_|

*/
