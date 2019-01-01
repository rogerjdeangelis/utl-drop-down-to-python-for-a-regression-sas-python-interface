# utl-drop-down-to-python-for-a-regression-sas-python-interface
Drop down to python for a regression.
    Drop down to python for a regression

    I used your data, but I had multiple syntax errors with the code that I was unable to fix.
    Could be my problem.

    github
    https://tinyurl.com/ydyjw89f
    https://github.com/rogerjdeangelis/utl-drop-down-to-python-for-a-regression-sas-python-interface

    Other python repos
    https://github.com/rogerjdeangelis?utf8=%E2%9C%93&tab=repositories&q=python+in%3Aname&type=&language=

    SAS Forum
    https://tinyurl.com/ybzfr2bd
    https://communities.sas.com/t5/SAS-Programming/python-to-SAS/m-p/523938

    INPUT (your data first and third column)
    =========================================

    options valivarname=v7;
    libname sd1 "d:/sd1";
    data sd1.have;
     input t7 t8 @@;
    cards4;
    30 -0.04978 60 -0.02080 90 -0.00485 120 -0.00300 150 -0.00098 180 0.00245 210
    0.00255 240 0.00357 270 0.00374 300 0.00905 330 0.01324 360 0.01406 390 0.01618
    420 0.01649 450 0.01114 480 0.01246 510 0.01284 540 0.00551 570 0.00288 600
    0.00323 630 0.00425 660 0.00736 690 0.00606 720 0.00373 750 0.00493 780 0.00435
    810 0.00404 840 0.00250 870 0.00308 900 0.00229 930 0.00198 960 0.00434 990
    0.00205 1020 0.00177 1050 0.00281 1080 0.00342 1110 0.00324 1140 0.00497 1170
    0.00498 1200 0.00537 1230 0.00546 1260 0.00475 1290 0.00547 1320 0.00609 1350
    0.00615 1380 0.00598 1410 0.00757 1440 0.00771 1470 0.00835 1500 0.00951 1530
    0.00956 1560 0.00881 1590 0.00835 1620 0.00848 1650 0.00590 1680 0.00903 1710
    0.01046 1740 0.00847 1770 0.01020 1800 0.01014 1830 0.00982 1860 0.01027 1890
    0.00880 1920 0.00807 1950 0.00648 1980 0.00286 2010 0.00517 2040 0.00293 2070
    0.02358 2100 0.00934 2130 -0.00731 2160 -0.01024 2190 -0.00854 2220 -0.02279
    2250 -0.01465 2280 -0.01331 2310 -0.01626 2340 -0.01912 2370 -0.02465 2400
    -0.02514 2430 -0.02776 2460 -0.02272 2490 -0.02323
    ;;;;
    run;quit;


    SD1.HAVE total obs=83

      Obs     T7        T8

        1      30    -0.04978
        2      60    -0.02080
        3      90    -0.00485
      .....
       81    2430    -0.02776
       82    2460    -0.02272
       83    2490    -0.02323


    EXAMPLE OUTPUT
    ==============

                                OLS Regression Results
    ==============================================================================
    Dep. Variable:                     T8   R-squared:                       0.072
    Model:                            OLS   Adj. R-squared:                  0.061
    Method:                 Least Squares   F-statistic:                     6.296
    Date:                Tue, 01 Jan 2019   Prob (F-statistic):             0.0141
    Time:                        16:34:20   Log-Likelihood:                 253.02
    No. Observations:                  83   AIC:                            -502.0
    Df Residuals:                      81   BIC:                            -497.2
    Df Model:                           1
    Covariance Type:            nonrobust
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    const          0.0072      0.003      2.814      0.006       0.002       0.012
    T7         -4.452e-06   1.77e-06     -2.509      0.014   -7.98e-06   -9.22e-07
    ==============================================================================
    Omnibus:                       48.725   Durbin-Watson:                   0.241
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              176.920
    Skew:                          -1.882   Prob(JB):                     3.82e-39
    Kurtosis:                       9.082   Cond. No.                     2.93e+03
    ==============================================================================

    Warnings:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 2.93e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.



    PROCESS
    =======

    %utl_submit_py64("
    import pandas as pd;
    import numpy as np;
    import statsmodels.api as sm;
    from sas7bdat import SAS7BDAT;
    have = pd.read_sas('d:/sd1/have.sas7bdat',encoding='ascii');
    X = have['T7'];
    y = have['T8'];
    X = sm.add_constant(X);
    model = sm.OLS(y, X).fit();
    predictions = model.predict(X);
    print(model.summary());
    ");

