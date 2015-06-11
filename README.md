# PROBer_paper_analysis

Reproduce PROBer paper analysis

### Prerequisites

Please make sure that you have `Perl`, `Python`, and `R` installed.

You need to install [Snakemake](https://bitbucket.org/johanneskoester/snakemake/wiki/Home). 

You also need to install [SRA Toolkit](http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software) in order to use [fastq-dump](http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc&f=fastq-dump).

### Reproduce analyses

#### Download Ding et al. read data from SRA 

You should put FASTQ files into `data/`.

Suppose you have `wget`, run the following commands:

```
cd data
wget ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR933/SRR933551/SRR933551.sra
wget ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR933/SRR933552/SRR933552.sra
wget ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR933/SRR933556/SRR933556.sra
wget ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR933/SRR933557/SRR933557.sra
```

Then run `fastq-dump` from SRA Toolkit to get FASTQ files:

```
fastq-dump SRR933551.sra 
fastq-dump SRR933552.sra 
fastq-dump SRR933556.sra 
fastq-dump SRR933557.sra 
```

The meaning of each data is listed in the table below:

<table>
        <tr>
                <th>accession</th>
                <th>meaning</th>
        </tr>
        <tr>
                <td>SRR933551</td>
                <td>Biological replicate I, (-) channel</td>
        </tr>
        <tr>
                <td>SRR933552</td>
                <td>Biological replicate I, (+) channel</td>
        </tr>
        <tr>
                <td>SRR933556</td>
                <td>Biological replicate II, (+) channel</td>
        </tr>
        <tr>
                <td>SRR933557</td>
                <td>Biological replicate II, (-) channel</td>
        </tr>
</table>

#### Run snakemake

Type

```
snakemake -j <number_of_threads>
```

in the top directory. `<number_of_threads>` is the total number of threads you want to use. 

##### Running time and memory usage measurement

Please make sure that your server has at least 40 cores. In addition, please do not run any **Python** scripts when you try to repeat the analysis. Otherwise, the time/memory measurements might be inaccurate and/or the snakemake may crash.
 