# The Minnesota COVID-19 Model

© 2020 Regents of the University of Minnesota. 

This software is licensed via the GNU General Public License 3.0.

More information: https://www.sph.umn.edu/research/projects/covid-19-model-code/ 

## How to use:
First, navigate to 'MNCOVID19/R' and open 'MNCOVID19.Rproj'. This will automatically set your working directory and ensure that the correct files are accessed by the various scripts in the repository.

Next, open the setup_model.R file ('MNCOVID19/R/setup_model.R') and ensure that all of the required packages are installed on your machine.

The primary script that is used to run the model and visualize the output is ‘R/scenarios_script.R’. Sourcing 'setup_model.R' at the top of the script will source all of the necessary model functions and load the required packages. Running the rest of the code in scenarios_script.R will run the model, print summaries of the model outputs for each strategy, and generate plots for visualizing outputs.

## Code orientation

Below is a general orientation to the primary .R files in this repository and the model functions they define:
- parameters_v3.R: Defines the function ```parameters()```, which is used to define and calculate model input parameters. The output is a list of parameters, which is then passed to other model functions.
- covid_19_model_function_v3.R: Defines the main model function, ```covid_19_model_function()```, which does some intermediate calculations on input parameters and calculates the change in compartments (i.e., dS, dE, dI, etc.) for one time step. Changes to the contact age-mixing matrix are applied within this function to reflect time-varying social distancing orders and policies.
- solve_model.R: Defines function ```solve_model()```, which takes as input model parameters and other simulation inputs (e.g. time horizon) and calls the ```covid_19_model_function()``` at each time step to determine the change in compartment sizes. It aggregates model output at each time step into a single output matrix.

Other .R files include:
- convert_parms.R: Defines the function ```convert_parms()``` that adjusts the subset of model parameters that need to be adjusted for the chosen model timestep (```parms$timestep```).
- lambda.R: Defines the function ```calculate_lambda()``` that calculates the age-specific force of infection given the current contact matrix and prevalence of infection.
- process_output_v3.R: Defines the function ```process_output()``` that extracts and saves measures of interest from raw model outputs (e.g. prevalence, daily deaths, ICU demand, cumulative infections, cumulative deaths, etc.).
