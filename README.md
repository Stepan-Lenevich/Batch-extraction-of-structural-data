# Batch-extraction-of-structural-data Perl Script
#This script converts data between Guassian specific .com and more widely used .xyz formats


#!/usr/bin/perl
$co_start=140; $co_end=290; $cs_start=180; $cs_end = 380;
$start = "Charge = -1 Multiplicity = 1";
$end = "Recover connectivity data from disk.";
$co=$co_start; $cs=$cs_start;
while ($co < $co_end){ while ($cs < $cs_end ){
# $in_file = "./" . $co . "/" . $co . "_" . $cs . "/All.out"; #linux
$in_file = ".\\" . $co . "\\" . $co . "_" . $cs . "\\All.out" ; #windows
$xyz_file = $co . "_" . $cs . ".xyz"; $out = $co . "_" . $cs . ".xyz";
print "read from $in_file and write to $out \n";
open( INIT, " < $in_file");
while (<INIT>){
if (/$start/){ $i=1; }
if (/$end/){ $i=0; close INIT ; }
if ($i==1){
@array = split(/,/, $_);
$out_line = " $array[0] $array[2] $array[3] $array[4]" ;
open( XYZ, " >> $xyz_file"); print XYZ $out_line ; close ( XYZ );
print $out_line ; }; }
$cs=$cs+10; } $cs=$cs_start; $co=$co+10;} print "Done\n";
