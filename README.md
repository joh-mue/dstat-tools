## dstat monitor plotting script

This ruby script uses GNUPlot through a ruby wrapper [(ruby_gnuplot)](https://github.com/rdp/ruby_gnuplot/blob/master/README.textile) to plot csv data generated by mvneves' [dstat-monitor](https://github.com/mvneves/dstat-monitor).

### Pre-requisites and Installation

You need an installation of the ruby programming language, X11, GNUPlot and the ruby_gnuplot gem. The gems csv and optparse are part of the ruby standard library.

To install on a Mac do the following steps:
```
1. Install XQuartz from here:
    http://xquartz.macosforge.org/landing/
2. Install gnuplot with homebrew:
    brew install gnuplot --with-x11
3. Install gnuplot gem:
    gem install gnuplot
```

For linux the procedure is
```
1. Install gnuplot (your distribution might come with it though)
    sudo apt-get install gnuplot
2. Install gnuplot gem:
    gem install gnuplot
3. Install csv gem
    gem install fastercsv
```

### Usage

```
Usage: dstat_plot.rb [options] -c CATEGORY -f FIELD [directory | file1 file2 ...]
    -v, --verbose                    Output more information
    -i, --invert [VALUE]             Invert the graph such that inverted(x) = VALUE - f(x), default is 100
    -n, --no-key                     No plot key is printed
    -d, --dry                        Dry run. Plot is not saved to file but displayed with gnuplot
    -o, --output PATH                Path where the graph should be saved to, default is csv file directory
    -y, --y-range RANGE              Sets the y-axis range. Default is 105 or "autoscale" if a value exceeds the set range
    -c, --category CATEGORY          Select the category
    -f, --field FIELD                Select the field
    -h, --help                       Display this screen
```

(-c CATEGORY and -f FIELD are mandatory parameters)

The plot is saved as category-field.png in the folder where the csv files are located unless -o PATH explicitly specifies a different destination.

### Example

```
ruby dstat_plot.rb -c "total cpu usage" -f "usr" example.csv
```

### Possible category - field combinations

(N is the cpu core index for 0..n cores)

Categoriy | Field |   | Categoriy | Field |
----------|-------|---| ----------|-------|
epoch     | epoch |   | net/total | recv
memory usage | used | |           | send
          | buff  |   | net/eth0  | recv
          | cach  |   |           | send
          | free  |   | dsk/total | read
swap      | used  |   |           | writ
          |free   |   | dsk/sda   | read
system    | int   |   |           | writ
          |csv    |   | io/total  | read
paging    | in    |   |           | writ
          |out    |   | io/sda    | read
total cpu usage   | usr | |       | writ
          | sys
          | idl
          | wai
          | hiq
          | siq
cpuN usage | usr
          | sys
          | idl
          | wai
          | hiq
          | siq
