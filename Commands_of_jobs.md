## Create Interactive jobs:
```qsub -X -I -l select=1:ncpus=36:mpiprocs=36 -l walltime=01:00:00 -q regular -A project_code```

