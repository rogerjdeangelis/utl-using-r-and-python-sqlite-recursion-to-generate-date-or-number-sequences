# utl-using-r-and-python-sqlite-recursion-to-generate-date-or-number-sequences
Using r and python sqlite recursion to generate date or number sequences 
    %let pgm=utl-using-r-and-python-sqlite-recursion-to-generate-date-or-number-sequences;

    Using r and python sqlite recursion to generate date or number sequences

        Three examples of sqlite in r and python (only r shown)

              1 sequence 1 to 10
              2 12 month sequence
              3 fibonacci sequence

       SAS monotonic and my sqlpartition macro can add sequences to a table
       sqlite partition clause can aslo add sequences to a table

    github
    https://tinyurl.com/yc5je5uv
    https://github.com/rogerjdeangelis/utl-using-r-and-python-sqlite-recursion-to-generate-date-or-number-sequences

    /*                                              _   _          _  ___
    / |  ___  ___  __ _ _   _  ___ _ __   ___ ___  / | | |_ ___   / |/ _ \
    | | / __|/ _ \/ _` | | | |/ _ \ `_ \ / __/ _ \ | | | __/ _ \  | | | | |
    | | \__ \  __/ (_| | |_| |  __/ | | | (_|  __/ | | | || (_) | | | |_| |
    |_| |___/\___|\__, |\__,_|\___|_| |_|\___\___| |_|  \__\___/  |_|\___/
                     |_|
    */


    %utl_rbegin;
    parmcards4;
    library(sqldf)
    res<-sqldf("
    WITH RECURSIVE cnt(x) AS (
      SELECT 1
      UNION ALL
      SELECT x+1 FROM cnt WHERE x < 10
    )
    SELECT x FROM cnt;
    ")
    str(res)
    res
    ;;;;
    %utl_rend;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   > str(res)                                                                                                           */
    /*   dataframe                                                                                                            */
    /*    $ x: int  1 2 3 4 5 6 7 8 9 10                                                                                      */
    /*   > res                                                                                                                */
    /*       x                                                                                                                */
    /*   1   1                                                                                                                */
    /*   2   2                                                                                                                */
    /*   3   3                                                                                                                */
    /*   4   4                                                                                                                */
    /*   5   5                                                                                                                */
    /*   6   6                                                                                                                */
    /*   7   7                                                                                                                */
    /*   8   8                                                                                                                */
    /*   9   9                                                                                                                */
    /*   10 10                                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___    _ ____                          _   _
    |___ \  / |___ \   _ __ ___   ___  _ __ | |_| |__    ___  ___  __ _ _   _  ___ _ __   ___ ___
      __) | | | __) | | `_ ` _ \ / _ \| `_ \| __| `_ \  / __|/ _ \/ _` | | | |/ _ \ `_ \ / __/ _ \
     / __/  | |/ __/  | | | | | | (_) | | | | |_| | | | \__ \  __/ (_| | |_| |  __/ | | | (_|  __/
    |_____| |_|_____| |_| |_| |_|\___/|_| |_|\__|_| |_| |___/\___|\__, |\__,_|\___|_| |_|\___\___|
                                                                     |_|
    */

    %utl_rbegin;
    parmcards4;
    library(sqldf)
    res<-sqldf("
    WITH RECURSIVE dates(x) AS (
      SELECT '2015-01-01'
      UNION ALL
      SELECT DATE(x, '+1 MONTHS') FROM dates WHERE x < '2016-01-01'
    )
    SELECT * FROM dates;
    ")
    res
    ;;;;
    %utl_rend;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  > res                                                                                                                 */
    /*              x                                                                                                         */
    /*  1  2015-01-01                                                                                                         */
    /*  2  2015-02-01                                                                                                         */
    /*  3  2015-03-01                                                                                                         */
    /*  4  2015-04-01                                                                                                         */
    /*  5  2015-05-01                                                                                                         */
    /*  6  2015-06-01                                                                                                         */
    /*  7  2015-07-01                                                                                                         */
    /*  8  2015-08-01                                                                                                         */
    /*  9  2015-09-01                                                                                                         */
    /*  10 2015-10-01                                                                                                         */
    /*  11 2015-11-01                                                                                                         */
    /*  12 2015-12-01                                                                                                         */
    /*  13 2016-01-01                                                                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____    __ _ _                                _
    |___ /   / _(_) |__   ___  _ __   __ _  ___ ___(_)  ___  ___  __ _ _   _  ___ _ __   ___ ___
      |_ \  | |_| | `_ \ / _ \| `_ \ / _` |/ __/ __| | / __|/ _ \/ _` | | | |/ _ \ `_ \ / __/ _ \
     ___) | |  _| | |_) | (_) | | | | (_| | (_| (__| | \__ \  __/ (_| | |_| |  __/ | | | (_|  __/
    |____/  |_| |_|_.__/ \___/|_| |_|\__,_|\___\___|_| |___/\___|\__, |\__,_|\___|_| |_|\___\___|
                                                                    |_|
    */

    %utl_rbegin;
    parmcards4;
    library(sqldf)
    res<-sqldf('
      with recursive fibo as (
        select 0 as a, 1 as b, 1 as i
        union all
        select b, a+b, i+1
        from fibo
        where i < 10
      )
      select a as fib
      from fibo')
    res
    ;;;;
    %utl_rend;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  > res                                                                                                                 */
    /*     fib                                                                                                                */
    /*  1    0                                                                                                                */
    /*  2    1                                                                                                                */
    /*  3    1                                                                                                                */
    /*  4    2                                                                                                                */
    /*  5    3                                                                                                                */
    /*  6    5                                                                                                                */
    /*  7    8                                                                                                                */
    /*  8   13                                                                                                                */
    /*  9   21                                                                                                                */
    /*  10  34                                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
