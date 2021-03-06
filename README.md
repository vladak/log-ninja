log-ninja
=========

A set of scripts I find useful when analysing log files

distribution
------------

See <a href="http://bit.ly/pivot-stdout"> for more information about this script.

Briefly, use it like this:

Show distribution of earthquake magnitudes over the last 7 days:
<pre>
mark$ curl http://earthquake.usgs.gov/earthquakes/catalogs/eqs7day-M0.txt --silent \
| \sed '1d' \
| cut -d, -f9 \
| distribution -v max_width=80
   Value   Height     %ile Histogram
       0      274  23.7435 #########################################
       1      545  70.9705 ################################################################################
       2      196  87.9549 #############################
       3       45  91.8544 #######
       4       59  96.9671 #########
       5       31  99.6534 #####
       6        4 100.0000 #
</pre>

Or show the distribution of word length in your UNIX dictionary:

<pre>
mark$ cat /usr/share/dict/words | awk '{print length($1)}' | distribution -v max_width=80
   Value   Height     %ile Histogram
       0        0   0.0000
       1       53   0.0110 #
       2     1271   0.2759 ##
       3     6221   1.5724 ########
       4    13208   4.3251 #################
       5    25102   9.5565 #################################
       6    41698  18.2467 ######################################################
       7    53944  29.4890 #####################################################################
       8    62334  42.4799 ################################################################################
       9    62615  55.5294 ################################################################################
      10    54667  66.9224 ######################################################################
      11    46512  76.6158 ############################################################
      12    37584  84.4486 #################################################
      13    27976  90.2790 ####################################
      14    19326  94.3067 #########################
      15    12160  96.8410 ################
      16     7137  98.3284 ##########
      17     4014  99.1649 ######
      18     2011  99.5840 ###
      19     1055  99.8039 ##
      20      508  99.9098 #
      21      240  99.9598 #
      22      103  99.9812 #
      23       50  99.9917 #
      24       19  99.9956 #
      25        9  99.9975 #
      26        2  99.9979 #
      27        3  99.9985 #
      28        2  99.9990 #
      29        2  99.9994 #
      30        1  99.9996 #
      31        1  99.9998 #
      32        0  99.9998
      33        0  99.9998
      34        0  99.9998
      35        0  99.9998
      36        0  99.9998
      37        0  99.9998
      38        0  99.9998
      39        0  99.9998
      40        0  99.9998
      41        0  99.9998
      42        0  99.9998
      43        0  99.9998
      44        0  99.9998
      45        1 100.0000 #
</pre>

It's <a href="http://en.wikipedia.org/wiki/Pneumonoultramicroscopicsilicovolcanoconiosis">pneumonoultramicroscopicsilicovolcanoconiosis</a> by the way, in case you were wondering. I thought you were.

You could cut out the outlier by selecting a window of values (i.e. min and max) like this:

<pre>
mark$ cat /usr/share/dict/words | awk '{print length($1)}' | distribution -v max_width=80 -v max=31 -v min=3
</pre>

But please note that the percentiles will not be correct if you specify a min or a max value - this is a known bug and might get fixed if I rewrite it to make it more readable.
