---
layout: manualsection
title: Detection of recombination block in signal
permalink: 07-manual.html
manual: true
published: true
status: publish
---
 

 
Having scanned for recombination signal for the desired sequence triplets, the `BlockDetection` step is executed using the `findBlocks` method.
 
This step identifies regions of recombination in a given sequence triplet by examining the data from the sliding window scans in the previous `SSAnalysis` step. If there are any regions in which two sequences meet a certain sequence similarity threshold, they are treated as potentially recombinant.
 
The parameters for this step are:
 
ManualThresholds
  : A vector of numbers between 0 and 100.
  : Each is a percenage sequence similarity threshold.
  : These thresholds are set by the user, and can be used to find recombination,
  : or used as a fallback if HybRIDS fails to automatically decide on some thresholds.
  
AutoThresholds
  : A logical argument (`TRUE`, or `FALSE`), if `TRUE` (default) then during execution of the `findBlocks` method,
  : thresholds will be decided on automatically. If `FALSE` then the `ManualThresholds` will be used.
  
ManualFallback
  : A logical argument (`TRUE`, or `FALSE`), if `TRUE` (default), then if automatic thresholds cannot be found, the
  : `ManualThresholds` will be used instead.
  
SDstringency
  : A numeric value, the higher it is, the closer automatically detected thresholds are allowed to be to the mean
  : sequence similarity across the sequences. It is usually fine to leave this as 2.
  
Like the `analyzeSS` method in the previous section, the `findBlocks` must be given an argument that dictates which triplets of the set defined by the `TripletGeneration` parameters will have blocks found from their scan data.
By default this is set to `"NOT.SEARCHED"` which will find blocks for triplets which have not already had blocks identified from their scan data. This argument can also be set to `"ALL"` or a list of vectors that each contain three sequence names.
 
The below example finds blocks in the two triplets that were scanned for recombination signal in the previous section:

    tripletsToSearch <- list(c("Seq1", "Seq4", "Seq7"), c("Seq1", "Seq4", "Seq8"))
    MyAnalysis$findBlocks(tripletsToSearch)

    ## Using the autodetect thresholds method...
    ## Deciding on suitable thresholds...
    ## Now beginning Block Search...
    ## Using the autodetect thresholds method...
    ## Deciding on suitable thresholds...
    ## Now beginning Block Search...
    ## Finished finding potential blocks for all triplet selections.
 
 
 