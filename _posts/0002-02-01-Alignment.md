---
feature_text: |
  ## Precision Medicine
title: Alignment
categories:
    - Module 2
feature_image: "assets/genvis-dna-bg_optimized_v1a.png"
date: 0002-02-01
---

WGS and Exome fastq data will be aligned with BWA MEM using the following options:

- t: number of threads
- Y: use soft clipping for supplementary alignments
- R: read group header line info. See table below for sample details.

| Data | Readgroup ID | Platform | FC[-BC].Lane | Library | Sample Name |
|-----|--------------|----------|------------|---------|-------------|
| Exome_Norm | 2891351068 | Illumina | C1TD1ACXX-CGATGT.7 | exome_norm_lib1 | HCC1395BL_DNA |
| Exome_Tumor | 2891351066 | Illumina | C1TD1ACXX-ATCACG.7 | exome_tumor_lib1 | HCC1395_DNA |
| RNAseq_Norm_Lane1 | 2895625992 | Illumina | H3MYFBBXX-CTTGTA.4 | rna_norm_lib1 | HCC1395BL_RNA |
| RNAseq_Norm_Lane2 | 2895626097 | Illumina | H3MYFBBXX-CTTGTA.5 | rna_norm_lib1 | HCC1395BL_RNA |
| RNAseq_Tumor_Lane1 | 2895626107 | Illumina | H3MYFBBXX-GCCAAT.4 | rna_tumor_lib1 | HCC1395_RNA |
| RNAseq_Tumor_Lane2 | 2895626112 | Illumina | H3MYFBBXX-GCCAAT.5 | rna_tumor_lib1 | HCC1395_RNA |
| WGS_Norm_Lane1 | 2891323123 | Illumina | D1VCPACXX.6 | wgs_norm_lib1 | HCC1395BL_DNA |
| WGS_Norm_Lane2 | 2891323124 | Illumina | D1VCPACXX.7 | wgs_norm_lib2 | HCC1395BL_DNA |
| WGS_Norm_Lane3 | 2891323125 | Illumina | D1VCPACXX.8 | wgs_norm_lib3 | HCC1395BL_DNA |
| WGS_Tumor_Lane1 | 2891322951 | Illumina | D1VCPACXX.1 | wgs_tumor_lib1 | HCC1395_DNA |
| WGS_Tumor_Lane2 | 2891323174 | Illumina | D1VCPACXX.2 | wgs_tumor_lib1 | HCC1395_DNA |
| WGS_Tumor_Lane3 | 2891323175 | Illumina | D1VCPACXX.3 | wgs_tumor_lib2 | HCC1395_DNA |
| WGS_Tumor_Lane4 | 2891323150 | Illumina | D1VCPACXX.4 | wgs_tumor_lib2 | HCC1395_DNA |
| WGS_Tumor_Lane5 | 2891323147 | Illumina | D1VCPACXX.5 | wgs_tumor_lib3 | HCC1395_DNA |
|-----|--------------|----------|------------|---------|-------------|

### Run bwa mem using the above information

Runtimes: Exome, 20 - 25min (32 cores); WGS, 89-95min (32 cores); WGS, 196-223min (16 cores) 

```bash
cd ~/data
mkdir alignment
cd alignment
bwa mem -t 32 -Y -R "@RG\tID:2891351068\tPL:ILLUMINA\tPU:C1TD1ACXX-CGATGT.7\tLB:exome_norm_lib1\tSM:HCC1395BL_DNA" -o /home/ubuntu/data/alignment/Exome_Norm.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/Exome_Norm/2891351068_1.fastq.gz /home/ubuntu/data/fastqs/Exome_Norm/2891351068_2.fastq.gz
bwa mem -t 32 -Y -R "@RG\tID:2891351066\tPL:ILLUMINA\tPU:C1TD1ACXX-ATCACG.7\tLB:exome_tumor_lib1\tSM:HCC1395_DNA" -o /home/ubuntu/data/alignment/Exome_Tumor.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/Exome_Tumor/2891351066_1.fastq.gz /home/ubuntu/data/fastqs/Exome_Tumor/2891351066_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323123\tPL:ILLUMINA\tPU:D1VCPACXX.6\tLB:wgs_norm_lib1\tSM:HCC1395BL_DNA" -o /home/ubuntu/data/alignment/WGS_Norm_Lane1.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Norm/2891323123_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Norm/2891323123_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323124\tPL:ILLUMINA\tPU:D1VCPACXX.7\tLB:wgs_norm_lib2\tSM:HCC1395BL_DNA" -o /home/ubuntu/data/alignment/WGS_Norm_Lane2.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Norm/2891323124_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Norm/2891323124_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323125\tPL:ILLUMINA\tPU:D1VCPACXX.8\tLB:wgs_norm_lib3\tSM:HCC1395BL_DNA" -o /home/ubuntu/data/alignment/WGS_Norm_Lane3.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Norm/2891323125_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Norm/2891323125_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891322951\tPL:ILLUMINA\tPU:D1VCPACXX.1\tLB:wgs_tumor_lib1\tSM:HCC1395_DNA" -o /home/ubuntu/data/alignment/WGS_Tumor_Lane1.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Tumor/2891322951_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Tumor/2891322951_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323174\tPL:ILLUMINA\tPU:D1VCPACXX.2\tLB:wgs_tumor_lib1\tSM:HCC1395_DNA" -o /home/ubuntu/data/alignment/WGS_Tumor_Lane2.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Tumor/2891323174_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Tumor/2891323174_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323175\tPL:ILLUMINA\tPU:D1VCPACXX.3\tLB:wgs_tumor_lib2\tSM:HCC1395_DNA" -o /home/ubuntu/data/alignment/WGS_Tumor_Lane3.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Tumor/2891323175_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Tumor/2891323175_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323150\tPL:ILLUMINA\tPU:D1VCPACXX.4\tLB:wgs_tumor_lib2\tSM:HCC1395_DNA" -o /home/ubuntu/data/alignment/WGS_Tumor_Lane4.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Tumor/2891323150_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Tumor/2891323150_2.fastq.gz
bwa mem -t 16 -Y -R "@RG\tID:2891323147\tPL:ILLUMINA\tPU:D1VCPACXX.5\tLB:wgs_tumor_lib3\tSM:HCC1395_DNA" -o /home/ubuntu/data/alignment/WGS_Tumor_Lane5.sam /home/ubuntu/data/reference/GRCh38_full_analysis_set_plus_decoy_hla.fa /home/ubuntu/data/fastqs/WGS_Tumor/2891323147_1.fastq.gz /home/ubuntu/data/fastqs/WGS_Tumor/2891323147_2.fastq.gz
```

### Convert sam to bam format

Runtimes: Exome, 13min; 

```bash
cd ~/data/alignment
samtools view -h -b -o Exome_Norm.bam Exome_Norm.sam
samtools view -h -b -o Exome_Tumor.bam Exome_Tumor.sam
samtools view -h -b -o WGS_Norm_Lane1.bam WGS_Norm_Lane1.sam
samtools view -h -b -o WGS_Norm_Lane2.bam WGS_Norm_Lane2.sam
samtools view -h -b -o WGS_Norm_Lane3.bam WGS_Norm_Lane3.sam
samtools view -h -b -o WGS_Tumor_Lane1.bam WGS_Tumor_Lane1.sam
samtools view -h -b -o WGS_Tumor_Lane2.bam WGS_Tumor_Lane2.sam
samtools view -h -b -o WGS_Tumor_Lane3.bam WGS_Tumor_Lane3.sam
samtools view -h -b -o WGS_Tumor_Lane4.bam WGS_Tumor_Lane4.sam
samtools view -h -b -o WGS_Tumor_Lane5.bam WGS_Tumor_Lane5.sam
```

### Merge bam files

Run times: WGS_Norm, 86m; WGS_Tumor, 

```bash
cd ~/data/alignment
samtools merge -@ 4 WGS_Norm_merged.bam WGS_Norm_Lane1.bam WGS_Norm_Lane2.bam WGS_Norm_Lane3.bam
samtools merge -@ 4 WGS_Tumor_merged.bam WGS_Tumor_Lane1.bam WGS_Tumor_Lane2.bam WGS_Tumor_Lane3.bam WGS_Tumor_Lane4.bam WGS_Tumor_Lane5.bam
```

### Clean up un-needed sam/bam files

```bash
cd ~/data/alignment
rm /home/ubuntu/data/alignment/*.sam
rm /home/ubuntu/data/alignment/WGS_*_Lane*.bam

```

### Query name sort bam files

```bash
cd ~/data/alignment
samtools sort -@ 8 -n -o Exome_Norm_namesorted.bam Exome_Norm.bam
samtools sort -@ 8 -n -o Exome_Tumor_namesorted.bam Exome_Tumor.bam
samtools sort -@ 24 -n -o WGS_Norm_merged_namesorted.bam WGS_Norm_merged.bam
samtools sort -@ 24 -n -o WGS_Tumor_merged_namesorted.bam WGS_Tumor_merged.bam
```

### Mark duplicates

```bash
cd ~/data/alignment
java -Xmx64g -jar $PICARD MarkDuplicates I=Exome_Norm_namesorted.bam O=Exome_Norm_namesorted_mrkdup.bam ASSUME_SORT_ORDER=queryname METRICS_FILE=Exome_Norm_mrkdup_metrics.txt QUIET=true COMPRESSION_LEVEL=0 VALIDATION_STRINGENCY=LENIENT

java -Xmx64g -jar $PICARD MarkDuplicates I=Exome_Tumor_namesorted.bam O=Exome_Tumor_namesorted_mrkdup.bam ASSUME_SORT_ORDER=queryname METRICS_FILE=Exome_Tumor_mrkdup_metrics.txt QUIET=true COMPRESSION_LEVEL=0 VALIDATION_STRINGENCY=LENIENT
java -Xmx64g -jar $PICARD MarkDuplicates I=WGS_Norm_merged_namesorted.bam O=WGS_Norm_merged_namesorted_mrkdup.bam ASSUME_SORT_ORDER=queryname METRICS_FILE=Exome_Norm_mrkdup_metrics.txt QUIET=true COMPRESSION_LEVEL=0 VALIDATION_STRINGENCY=LENIENT
java -Xmx64g -jar $PICARD MarkDuplicates I=WGS_Tumor_merged_namesorted.bam O=WGS_Tumor_merged_namesorted_mrkdup.bam ASSUME_SORT_ORDER=queryname METRICS_FILE=Exome_Norm_mrkdup_metrics.txt QUIET=true COMPRESSION_LEVEL=0 VALIDATION_STRINGENCY=LENIENT
```

### Position sort bam file

```bash
cd ~/data/alignment
samtools sort -o Exome_Norm_sorted_mrkdup.bam Exome_Norm_namesorted_mrkdup.bam
samtools sort -o Exome_Tumor_sorted_mrkdup.bam Exome_Tumor_namesorted_mrkdup.bam
samtools sort -o WGS_Norm_merged_sorted_mrkdup.bam WGS_Norm_merged_namesorted_mrkdup.bam
samtools sort -o WGS_Tumor_merged_sorted_mrkdup.bam WGS_Tumor_merged_namesorted_mrkdup.bam
```

### Perform Base Quality Score Recalibration 



### Index bam file

```bash
cd ~/data/alignment
samtools index Exome_Norm_2891351068.sorted.cram
```


