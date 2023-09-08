# ibex

A tool to explore the effects of the Iberian exception mechanism on inflation. The script `main.R` replicates the figures and tables in *Haro-Ruiz, M., Schult, C. & Wunder, C. (2023). The effects of the Iberian Exception mechanism on wholesale electricity prices and consumer inflation. A synthetic-controls approach*. 

## Deploy

ibex can be deployed in a docker container.  To do so, you must have [Docker](https://www.docker.com/) installed in your machine.

Begin by cloning this repository form the command line: 

```shell
git clone https://github.com/mharoruiz/ibex && \
cd ibex
```

Make sure your working directory points to the cloned repository. You can check this with `pwd` (Linux) or `cd` (Windows). 

Next, run a Docker container from an image that contains all the necessary dependencies: 

```shell
docker run --rm \
-p 8787:8787 \
-e DISABLE_AUTH=true \
-v $(pwd):/home/rstudio/ibex \
-v /home/rstudio/ibex/renv mharoruiz/ibex:0.1
```

The above command runs the container (`docker run`) from the image (`mharoruiz/ibex:0.1`), and mounts the local project directory into the container directory (`-v $(pwd):/home/rstudio/ibex`). Depending on your operating system, you may need to use `%cd%` instead of `$(pwd)`.

You can now access the container by pointing your browser to `localhost:8787`. This will open an instance of RStudio which is ready to reproduce the results. 

Open `ibex/ibex.Rproj` to load the project dependencies. The following message should appear in your R console:

```R
- Project '~/ibex' loaded. [renv 1.0.2]
```

## Replicate

`ibex/main.R` replicates the figures and tables in Haro-Ruiz, M., Schult, C. & Wunder, C. Adjust the value of constant `PRC_STEP` in line 18 to regulate the script's runtime. Execute the script by pressing Cmd/Ctrl + Shift + S or using the following command:

```R
source("~/ibex/main.R")
```

Once `main.R` has successfully run, the figures and tables will be accessible as variables in your R environment, i.e. `fig_1`, `table_A1`. Additionally, if constant `SAVE_ANALYSIS=TRUE`, the figures and tables will be saved to `04_analysis\` as .png and .csv, respectively.

