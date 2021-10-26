# hse21_hw1

Шагалкина Дарья, группа 1

### Список всех команд, выполненных на сервере

    mkdir hw1
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L002_R1_001.fastq
    
    seqtk sample -s1213 oil_R1.fastq 5000000 > pe1.fastq
    seqtk sample -s1213 oil_R2.fastq 5000000 > pe2.fastq
    seqtk sample -s1213 oilMP_S4_L001_R1_001.fastq 1500000 > mp1.fastq
    seqtk sample -s1213 oilMP_S4_L001_R1_001.fastq 1500000 > mp2.fastq
    
    mkdir fastqc
    ls *.fastq | xargs -P 4 -tI{} fastqc -o fastqc {}
    
    mkdir multiqc
    multiqc -o multiqc fastqc
    
    platanus_trim pe*.fastq
    platanus_internal_trim mp*.fastq
    
    rm pe*.fastq 
    rm mp*.fastq
    
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/pe1_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/pe2_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/mp1_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/mp2_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/multiqc/multiqc_report.html /home/daria/Documents/minor
    
    rm *fastqc.html
    rm multiqc_report.html
    
    ls *.trimmed | xargs -P 4 -tI{} fastqc -o fastqc {}
    ls *.int_trimmed | xargs -P 4 -tI{} fastqc -o fastqc {}
    multiqc -o multiqc fastqc
    
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/pe1.fastq.trimmed_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/pe2.fastq.trimmed_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/mp1.fastq.int_trimmed_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/fastqc/mp2.fastq.int_trimmed_fastqc.html /home/daria/Documents/minor
    scp -i my_key -P 32222 dvshagalkina@92.242.58.92:/home/dvshagalkina/hw1/multiqc/multiqc_report.html /home/daria/Documents/minor
    
    
    
    
    
    
