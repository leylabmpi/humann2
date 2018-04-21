Overview of changes to the humann2 pipeline

# humann2 pipeline outline

* main
  * prescreen.alignment
    * `metaphlan2`
      * input: fastq reads
      * output: *_metaphlan_bowtie2.txt, *_metaphlan_bugs_list.tsv
        * bug_file, bowtie2_out
  * prescreen.create_custom_database
    * input: bug_file
    * output: custom_database (*.ffn)
  * nucleotide.index
    * input: custom_database
    * output: index_name (bowtie2 index)
  * nucleotide.alignment
    * runs bowtie2 vs custom_database
      * add?: samtools view -bS eg2.sam > eg2.bam
      * change?: `keep_sam = False`
      * input: fastq reads, index_name, (custom_database)
	* output: sam file
    * remove: bowtie2 index
  * nucleotide.unaligned_reads
    * input: sam file
    * output: unaligned reads (& unaligned object)
  *  gene_families
    * compute from alignments
      * output: genefamilies file


# conda dev env

humann2_dev = `conda create -n humann2_dev "bowtie2>=2.2.5" "metaphlan2>=2.6.0" "diamond>=0.7.10,<0.9.0" samtools biom-format matplotlib scipy numpy`


