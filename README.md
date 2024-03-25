# utl-load-an-entire-file-into-a-r-string
    %let pgm=utl-load-an-entire-file-into-a-r-string;

    Load an entire file into a r string of length over one hunfred thousand bytes

    Problem
      Output  substr("d:/txt/fyl,txt",63995,64008)

      Note I have 138gb ram.

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                                      |                                  |                              */
    /*                    INPUT                             |        PROCESS                   |      OUTPUT                  */
    /*                                                      |                                  |                              */
    /* data _null_;                                         |  %utl_submit_r64x('              |  "FILE LENGTH"               */
    /*   length txt1 txt2 $32000;                           |  library(readr);                 |  128004 (two cr/lf strings)  */
    /*   txt1=repeat('1111111111',3199); /* 32,000 bytes */ |  mystring <-                     |                              */
    /*   txt2=repeat('9999999999',3199); /* 32,000 bytes */ |    read_file("d:/txt/fyl,txt");  |  "substr([file],63995,64008)"*/
    /*   file "d:/txt/fyl,txt" lrecl=64000 recfm=v;         |  "FILE LENGTH";                  |                              */
    /*   put txt1 +(-1) txt1;                               |  nchar(mystring);                |  "111111\r\n999999"          */
    /*   put txt2 +(-1) txt2;                               |  "substr(mystring,63995,64008)"; |                              */
    /* run;quit;                                            |  substr(mystring,63995,64008);   |  Note                        */
    /*                                                      |  ');                             |    line1 is 64000 '1's       */
    /* NOTE: 2 records written to the file "d:/txt/fyl,txt".|                                  |    line1 is 64000 '9's       */
    /*       The minimum record length was 64000.           |                                  |                              */
    /*       The maximum record length was 64000.           |                                  |  We are brifging the two     */
    /*                                                      |                                  |  lines.                      */
    /* d:/txt/fyl,txt                                       |                                  |                              */
    /*                                                      |                                  |                              */
    /* File with two long lines of length 64,000 bytes each |                                  |                              */
    /*                                                      |                                  |                              */
    /* 1111111111111111111111111111111111111111111111111... |                                  |                              */
    /* 9999999999999999999999999999999999999999999999999... |                                  |                              */
    /*                                                      |                                  |                              */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data _null_;
      length txt1 txt2 $32000;
      txt1=repeat('1111111111',3199); /* 32,000 bytes */
      txt2=repeat('9999999999',3199); /* 32,000 bytes */
      file "d:/txt/fyl,txt" lrecl=64000 recfm=v;
      put txt1 +(-1) txt2;
      put txt1 +(-1) txt2;
    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* File with two long lines of length 64,000 bytes                                                                        */
    /*                                                                                                                        */
    /* 1111111111111111111111111111111111111111111111111...  64,000 + 2 for cr/lf                                             */
    /* 9999999999999999999999999999999999999999999999999...  64,000 + 2 for cr/lf                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utl_submit_r64x('
    library(readr);
    mystring <-
      read_file("d:/txt/fyl,txt");
    "FILE LENGTH";
    nchar(mystring);
    "substr(mystring,63995,64008)";
    substr(mystring,63995,64008);
    ');

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*       OUTPUT                                                                                                           */
    /*                                                                                                                        */
    /*   "FILE LENGTH"                                                                                                        */
    /*   128004 (+ two cr/lf strings)                                                                                         */
    /*                                                                                                                        */
    /*   "substr([file],63995,64008)"                                                                                         */
    /*                                                                                                                        */
    /*   "111111\r\n999999"                                                                                                   */
    /*                                                                                                                        */
    /*   Note                                                                                                                 */
    /*     line1 is 64000 '1's                                                                                                */
    /*     line1 is 64000 '9's                                                                                                */
    /*                                                                                                                        */
    /*   We are brifging the two                                                                                              */
    /*   lines.                                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
Load an entire file into a r string of length over one hunfred thousand bytes
