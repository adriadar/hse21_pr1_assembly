# hse21_hw1

Шагалкина Дарья, группа 1

## Список команд

    mkdir hw1
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
    
    seqtk sample -s25 oil_R1.fastq 5000000 > pe1.fastq
    seqtk sample -s25 oil_R2.fastq 5000000 > pe2.fastq
    seqtk sample -s25 oilMP_S4_L001_R1_001.fastq 1500000 > mp1.fastq
    seqtk sample -s25 oilMP_S4_L001_R2_001.fastq 1500000 > mp2.fastq
    
    rm oil*
    mkdir fastqc
    fastqc *.fastq
    
    mkdir multiqc
    multiqc -o multiqc fastqc
    
    platanus_trim pe*.fastq
    platanus_internal_trim mp*.fastq
    
    rm *.fastq 
   
    fastqc *.trimmed
    fastqc *.int_trimmed
    mkdir fastqc_tr
    mv *.zip fastqc_tr
    mv *.html fastqc_tr
    
    mkdir multiqc_tr
    multiqc -o multiqc_tr fastqc_tr
    
    platanus assemble -f pe1.fastq.trimmed pe2.fastq.trimmed
    platanus scaffold -c out_contig.fa -IP1 pe1.fastq.trimmed pe2.fastq.trimmed -OP2 mp1.fastq.int_trimmed mp2.fastq.int_trimmed
    platanus gap_close -c out_scaffold.fa -IP1 pe1.fastq.trimmed pe2.fastq.trimmed -OP2 mp1.fastq.int_trimmed mp2.fastq.int_trimmed
    
    sed -n '1,/>/p' out_scaffold.fa | cat >longest.fasta
    sed -i '$d' longest.fasta
    
    sed -n '1,/>/p' out_gapClosed.fa | cat >longest_without_gaps.fasta
    sed -i '$d' longest_without_gaps.fasta
    
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw2/multiqc/multiqc_report.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw2/multiqc_tr/multiqc_report.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw2/out* /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw2/close_gaps/long* /home/daria/Documents/minor
    
    

## MultiQC отчет
#### Для не подрезанных чтений
[ссылка на полный отчет](https://github.com/adriadar/hse21_hw1/blob/main/MultiQC_report/not_trimmed_multiqc_report.html)
![image](https://github.com/adriadar/hse21_hw1/blob/main/MultiQC_report/not_trimmed_general_statistics.png)
![image](https://github.com/adriadar/hse21_hw1/blob/main/MultiQC_report/not_trimmed_per_sequence_quality_scores_plot.png)

#### Для подрезанных чтений
[ссылка на полный отчет](https://github.com/adriadar/hse21_hw1/blob/main/MultiQC_report/trimmed_multiqc_report.html)
![image](https://github.com/adriadar/hse21_hw1/blob/main/MultiQC_report/trimmed_general_statistics.png)
![image](https://github.com/adriadar/hse21_hw1/blob/main/MultiQC_report/trimmed_per_sequence_quality_scores_plot.png)

## Анализ
[colab с кодом для анализа контигов, скаффолдов и гэпов](https://colab.research.google.com/drive/1ip5FUUN57o337_16wI4cx-0sK598CsDy?usp=sharing)
