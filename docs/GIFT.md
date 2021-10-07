GIFT is an application supported by the NIH under grant 1RO1EB000840 to
Dr. Vince Calhoun and Dr. Tulay Adali. It is a MATLAB toolbox which
implements multiple algorithms for independent component analysis and
blind source separation of group (and single subject) functional
magnetic resonance imaging data.

## Using GIFT GUI

### Run Matlab GUI

First, [prepare to run GUI
application](Running_GUI_applications "wikilink"). Then run the Matlab
GUI using one of the following:

Method 1 (via SLURM X11):

`$ module load Framework/Matlab2019b`
`$ srun -p qTRDEV -A PSYC0002 -v -n1 -c1 --mem=10g --export=TERM,HOME --pty --x11 /apps/Framework/MATLAB/R2019b/bin/matlab`

Method 2 (via interactive mode):

`$ srun -p qTRDEV -A PSYC0002 -v -n1 -c1 --mem=10g --pty --x11 /bin/bash `
`$ module load Framework/Matlab2019b`
`$ matlab &`

### Add GIFT path

`>> addpath(genpath('/trdapps/linux-x86_64/matlab/toolboxes/GroupICATv4.0b/'))`

### Run GIFT

`>> gift`

<figure>
<img src="Gift.png" title="Gift.png" width="800" alt="Gift.png" /><figcaption aria-hidden="true">Gift.png</figcaption>
</figure>

### Example analysis: Group ICA on auditory oddball data

Change to the data directory and create a folder. Then click "Setup ICA
Analysis" in GIFT and select the output folder.

`>> cd /data/users2/salman/mind/data/`
`>> mkdir ica_example/`

<figure>
<img src="Gift_select.png" title="Gift_select.png" width="800" alt="Gift_select.png" /><figcaption aria-hidden="true">Gift_select.png</figcaption>
</figure>

Select all subject data and all the ICA options.

<figure>
<img src="Gift_subject.png" title="Gift_subject.png" width="800" alt="Gift_subject.png" /><figcaption aria-hidden="true">Gift_subject.png</figcaption>
</figure>

Click the "Run Analysis" button in the GIFT window and start the
analysis.

<figure>
<img src="Gift_run.png" title="Gift_run.png" width="800" alt="Gift_run.png" /><figcaption aria-hidden="true">Gift_run.png</figcaption>
</figure>

Once analysis is done, visualize the output.

<figure>
<img src="Gift_result.png" title="Gift_result.png" width="800" alt="Gift_result.png" /><figcaption aria-hidden="true">Gift_result.png</figcaption>
</figure>

## Using GIFT Batch Scripts

Create the following batch script `gift_batch.m`:

`inputFile = '/path/to/input/file';`

`addpath( genpath( '/trdapps/linux-x86_64/matlab/toolboxes/GroupICATv4.0b/icatb/' ) )`
`icatb_batch_file_run(inputFile)`

Execute the script using the following commands (in a SLURM job script
or interactive node):

`$ module load Framework/Matlab2019b`
`$ matlab -batch 'gift_batch'`

### Serial/Parallel Mode

If you select `parallel_info.mode = 'serial';` in the GIFT batch input
file, you can increase the number of allocated CPUs in the SLURM job
script for faster analysis, e.g.

`#SBATCH -c 5`
`#SBATCH --mem=80g`

If you select `parallel_info.mode = 'parallel';` in the GIFT batch input
file, you can set the number of parallel pools equal to the number of
allocated CPUs (in the `#SBATCH -c` directive) in the SLURM job script,
e.g.

`# in job script `
`...`
`#SBATCH -c 5`

`# in batch input file`
`...`
`parallel_info.num_workers = 5;`

## Memory considerations

Note that GIFT tells you the amount of memory you need to run the
analysis. Please see [this section](Choosing_job_resources "wikilink")
for how to properly configure SLURM and Matlab for running the analysis
successfully.