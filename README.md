# Cibersort_docker
Run cibersort on docker

## Steps
1. Request access online https://cibersortx.stanford.edu/download.php (first column)
2. Install Docker Desktop (https://www.docker.com/products/docker-desktop) and make an account 
3. On local machine terminal
```
docker pull cibersortx/fractions
```
4. Obtain the token from the CIBERSORTx website (https://cibersortx.stanford.edu/getoken.php).
5. Make directory we will work in on local machine
```
cd /place/to/run/cibersort
mkdir Cibersort
cd Cibersort
mkdir Input
mkdir Output
```
6. Download LM22.txt reference from [cibersort website](https://cibersortx.stanford.edu/download.php) and move to `Cibersort/Input/` called `LM22.txt`
7. Copy mixture file (made using [cibersort_prep](https://github.com/shoffm/cibersort_prep)) to `Cibersort/Input/` called `cibersort_input_counts.tsv`
8. Navigate to directory with files to analyze and run. Don't forget to update your email and token where it is noted in the code below
```
cd Cibersort
docker run -v Cibersort/Input:/src/data -v Cibersort/Output:/src/outdir cibersortx/fractions --username <ADD YOUR EMAIL> --token <ADD YOUR TOKEN> --mixture cibersort_input_counts.tsv --sigmatrix LM22.txt --rmbatchBmode TRUE --perm 100 --verbose TRUE --QN FALSE
```
9. Results will be in `Cibersort/Output`
   - `CIBERSORTx_Mixtures_Adjusted.txt` is the updated count matrix you input (in my case I gave it logCPM counts and it would reverse these)
   - `CIBERSORTx_Adjusted.txt` is the desired output matrix of cibersort imputed cell proportions
