# utl_how_to_calculate_difference_of_cholesterol_level_between_3_time_points
How to calculate difference of cholesterol level between 3 time points

    ```  How to calculate difference of cholesterol level between 3 time points                                                                                       ```
    ```                                                                                                                                                               ```
    ```    Calculate                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```       visit 2 - visit 1 Cholesterol_levels                                                                                                                    ```
    ```       visit 3 - visit 2 Cholesterol_levels                                                                                                                    ```
    ```       visit 3 - visit 1 Cholesterol_levels                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```       by id                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```    I don't think you can do easliy this using the SAS dif function because of grouping                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```    INPUT                                                                                                                                                      ```
    ```    =====                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```       WORK.HAVE total obs=9                |       RULES                                                                                                      ```
    ```                                            |                                                                                                                  ```
    ```                             CHOLESTEROL_   |                                                                                                                  ```
    ```       Obs    ID    VISIT        LEVEL      |                                                                                                                  ```
    ```                                            |                                                                                                                  ```
    ```        1      1      1            10       |                                                                                                                  ```
    ```        2      1      2            20       |    20 - 10  = 10                                                                                                 ```
    ```        3      1      3            30       |    30 - 20  = 10                                                                                                 ```
    ```                                            |    30 - 10  = 20                                                                                                 ```
    ```        4      2      1           100       |                                                                                                                  ```
    ```        5      2      2           200       |                                                                                                                  ```
    ```        6      2      3           300       |                                                                                                                  ```
    ```                                            |                                                                                                                  ```
    ```        7      3      1            10       |                                                                                                                  ```
    ```        8      3      2            10       |                                                                                                                  ```
    ```        9      3      3            10       |                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```        set have;                                                                                                                                              ```
    ```        by id;                                                                                                                                                 ```
    ```        select (visit);                                                                                                                                        ```
    ```           when (visit=1) val1=Cholesterol_level;                                                                                                              ```
    ```           when (visit=2) val2=Cholesterol_level;                                                                                                              ```
    ```           when (visit=3) do;                                                                                                                                  ```
    ```              val3=Cholesterol_level;                                                                                                                          ```
    ```              xval_2_minus_1=val2-val1;                                                                                                                        ```
    ```              xval_3_minus_2=val3-val2;                                                                                                                        ```
    ```              xval_3_minus_1=val3-val1;                                                                                                                        ```
    ```              output;                                                                                                                                          ```
    ```           end;                                                                                                                                                ```
    ```        end;                                                                                                                                                   ```
    ```        /* leave otherwise off to force error */                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      OUTPUT                                                                                                                                                   ```
    ```      ======                                                                                                                                                   ```
    ```                                      VAL_2_     VAL_3_     VAL_3_                                                                                             ```
    ```       VAL1    VAL2    VAL3    ID    MINUS_1    MINUS_2    MINUS_1                                                                                             ```
    ```                                                                                                                                                               ```
    ```         10      20      30     1       10         10         20                                                                                               ```
    ```        100     200     300     2      100        100        200                                                                                               ```
    ```         10      10      10     3        0          0          0                                                                                               ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  https://goo.gl/dTcq4u                                                                                                                                        ```
    ```  https://communities.sas.com/t5/General-SAS-Programming/How-to-calculate-difference-of-cholesterol-level-between-3-time/m-p/410384                            ```
    ```                                                                                                                                                               ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  data have;                                                                                                                                                   ```
    ```   input ID Visit Cholesterol_level;                                                                                                                           ```
    ```  cards4;                                                                                                                                                      ```
    ```  001 1 10                                                                                                                                                     ```
    ```  001 2 20                                                                                                                                                     ```
    ```  001 3 30                                                                                                                                                     ```
    ```  002 1 100                                                                                                                                                    ```
    ```  002 2 200                                                                                                                                                    ```
    ```  002 3 300                                                                                                                                                    ```
    ```  003 1 10                                                                                                                                                     ```
    ```  003 2 10                                                                                                                                                     ```
    ```  003 3 10                                                                                                                                                     ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  * WPS;                                                                                                                                                       ```
    ```  %utl_submit_wps64('                                                                                                                                          ```
    ```  libname wrk sas7bdat "%sysfunc(pathname(work))";                                                                                                             ```
    ```  data wrk.wantwps(drop=visit Cholesterol_level);                                                                                                              ```
    ```    retain val1 val2 val3;                                                                                                                                     ```
    ```    set wrk.have;                                                                                                                                              ```
    ```    by id;                                                                                                                                                     ```
    ```    select (visit);                                                                                                                                            ```
    ```       when (1) val1=Cholesterol_level;                                                                                                                        ```
    ```       when (2) val2=Cholesterol_level;                                                                                                                        ```
    ```       when (3) do;                                                                                                                                            ```
    ```          val3=Cholesterol_level;                                                                                                                              ```
    ```          val_2_minus_1=val2-val1;                                                                                                                             ```
    ```          val_3_minus_2=val3-val2;                                                                                                                             ```
    ```          val_3_minus_1=val3-val1;                                                                                                                             ```
    ```          output;                                                                                                                                              ```
    ```       end;                                                                                                                                                    ```
    ```    end;                                                                                                                                                       ```
    ```    /* leave otherwise off to force error */                                                                                                                   ```
    ```  run;quit;                                                                                                                                                    ```
    ```  ');                                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  * SAS;                                                                                                                                                       ```
    ```  data want(drop=visit Cholesterol_level);                                                                                                                     ```
    ```    retain val1 val2 val3;                                                                                                                                     ```
    ```    set have;                                                                                                                                                  ```
    ```    by id;                                                                                                                                                     ```
    ```    select (visit);                                                                                                                                            ```
    ```       when (1) val1=Cholesterol_level;                                                                                                                        ```
    ```       when (2) val2=Cholesterol_level;                                                                                                                        ```
    ```       when (3) do;                                                                                                                                            ```
    ```          val3=Cholesterol_level;                                                                                                                              ```
    ```          val_2_minus_1=val2-val1;                                                                                                                             ```
    ```          val_3_minus_2=val3-val2;                                                                                                                             ```
    ```          val_3_minus_1=val3-val1;                                                                                                                             ```
    ```          output;                                                                                                                                              ```
    ```       end;                                                                                                                                                    ```
    ```    end;                                                                                                                                                       ```
    ```    /* leave otherwise off to force error */                                                                                                                   ```
    ```  run;quit;                                                                                                                                                    ```

