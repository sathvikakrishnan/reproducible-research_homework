# Reproducible research: version control and R

## Answers

__*Question 1-3*__
Here is the link to my logistic_growth repo 🔗 : 

__*Question 4*__
![Two Random Walks](https://github.com/sathvikakrishnan/logistic_growth/blob/ca91c0a223d46725fac2fe7159bf8e7706df4835/Random_Walk_Plot.png)

The random walks are depicted in two plots plotted side-by-side. The plots depict the paths of random walks over 500 steps. Despite both walks starting at 0,0, they have indivdiual trajectories with random angles due to the stochastic nature of Brownian motion in random walks. The directions are uncorrelated (i.e. the direction of movement is  independent of the previous directions moved) and unbiased (i.e. the direction of motion is random). As a result of these two features, the trajectories seem unpredictable and each path is unique. The colour variation along the paths represents the progression of time in both walks. Earlier steps are darker blue and later steps are lighter blue as indicated by the colour gradient key.

Random seeds are used in computational processes that involve randomness to ensure reproducibility. Also known as a seed state, or just seed, a random seed is a number (or vector) used to initialize a pseudorandom number. A random seed specifies the start point when a computer generates a random number sequence (Henkemans & Lee, 2001).

![Comparison of a script for reproducible simulation of Brownian motion and a scipt for simulating a random walk](https://github.com/sathvikakrishnan/reproducible-research_homework/blob/2bd4f6e93ccf30821287c3f49a0e688d0c4e56c5/comparison_2.png) 
![Comparison of a script for reproducible simulation of Brownian motion and a scipt for simulating a random walk](https://github.com/sathvikakrishnan/reproducible-research_homework/blob/94c2680173d2108e582beaa46f039f21c000676e/comparison_1.png)

__*Question 5*__

Number of Rows: 33 
Number of Columns: 13

As _V = β L<sup>α</sup>_, taking a logarithm of both sides will linearize the relationship. Therefore, the equation takes the form _log(V)=log(β)+αlog(L)_
By using a linear regression, I extracted these values from the summary table:

α (the exponent) = 1181.807

   This had a p value of less than 2.28 &times; 10<sup>-10</sup>. As this p-value is significatly less than any conventional significance level (e.g., 0.05 or 0.01), it can be concluded that there is very strong evidence against the null hypothesis so it is statistically significant.
   
β (the scaling factor) = 1.5152

   This had a p value of less than 6.44 &times; 10<sup>-10</sup>. As this p-value is significatly less than any conventional significance level (e.g., 0.05 or 0.01), it can be concluded that there is very strong evidence against the null hypothesis so it is statistically significant.

In [Table 2](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4093846/table/T2/?report=objectonly) of [Cui, Schlub and Holmes' 2014 paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4093846/), they report the allometric exponent for dsDNA (with 95% CI) to be 1.52 (1.16–1.87) and the scaling factor to be 1,182 (246–5,675). In comparison to my values, it appears that their exponent is similar to my scaling factor and their scaling factors is similar to my exponent. So it appears that I have interpreted what the scaling factor to be the exponent and visa versa.

#Renaming the columns to make them human readable

dsDNA_viruses <- dsDNA_viruses %>%

  rename(genome_length = Genome.length..kb., virion_vol = Virion.volume..nm.nm.nm.)
  
#Contents of the dsDNA_viruses data frame, showing the result of the column renaming

dsDNA_viruses 

#Fits a linear regression model using the lm function

model_linear <- lm(log(virion_vol) ~ log(genome_length), data = dsDNA_viruses)

#Summary of the linear regression model

summary(model_linear)

#Scatter plot which includes a shaded confidence interval. The line color is set to "blue", and the line width is set to 0.5.

ggplot(dsDNA_viruses, aes(x = log(genome_length), y = log(virion_vol)))+

  geom_point() +
  
  geom_smooth(method = "lm", se = TRUE, color = "blue", linewidth = 0.5) +
  
  labs(x = "log[Genome length (kb)]", y = "log[Virion volume (nn3)]") +
  
  theme_minimal()+ 
  
  theme(plot.background = element_rect(fill = "white", color = "grey", linewidth = 1),
   axis.line = element_line(color = "grey")) 
   
#Ensures that the axis are visible and the background is white with grid lines present

![Reproduced Graph](https://github.com/sathvikakrishnan/reproducible-research_homework/blob/2a7a8cebf1e598f38be903f534cf83a68e8ebd35/reproduced_plot_log.png)

The estimated volume of a 300kb dsDNA virus is 6697006nm<sup>3</sup>. To calculate this, I used _V = β L<sup>α</sup>_ where

α =  1.5152 
β = 1181.807  


__*Bonus Question*__
Replicability assesses the consistency in measurements conducted by a single individual within identical conditions (i.e. the ability to generate consistent results across different studies or experiments aiming to answer the same scientific question), whereas reproducibility gauges the ability to replicate an entire study or experiment in its entirety (i.e. the ability to re-run the same analysis on the same data and obtain the same results). Replicability validates the generalisability and robustness of scientific findings. If a study is replicable, then the results of the original study are reliable. Reproducability, on the other hand, is vital ritical for validating results and ensuring that findings are not dependent on specific conditions. If a study is reproducable, then the analysis was conducted fairly and correctly (Plesser 2017).

Git is a free and open source version control system (VCS). VCS manage the develop and evolution of a project. Specifically, Git is a Distributed Version Control System (DVCS) where every user has a complete repository called a local repoistory. Contrastingly, Centralised Version Control Systems (CVCS) have a central repository (Zolkifli et al 2018). Git also allows for non-linear development (i.e.  developers can work on different branches of code simultaneously and merge them together when complete). GitHub, on the other hand, is a web-based hosting service for Git repositories. In essence, it allows users and develop to share code with each other. Additionally, Github offers features such as bug tracking, task management, and project management.

Both Git and GitHub can be used to enhance reproducibility and replicability. Git improves reproudcibility by allowing users to track changes to code, data, and documentation through time. This means that different temporal versions of the code and data can be revisted, revised, and reproduced.Git also enables other users to access and develop code. In ensuring transparency, Git allows developers to replicate and reproduce results. The collaboratory aspect of GitHub also enhances reproducibility and replicability in scientific research. By providing a centralised platform for code/data/dcomunetaion sharing, GitHub facilitates reproducbility as researchers can reproduce analysis following the cloning of repositories. The open nature of GitHub also promotes transparency which improves replicability. Additionally to all of the above, both Git 'commits' and GitHub repositories serve as 'museums of code through time' (i.e. documentation of different versions of code increases reproducibility and replicability). 


## Instructions

The homework for this Computer skills practical is divided into 5 questions for a total of 100 points (plus an optional bonus question worth 10 extra points). First, fork this repo and make sure your fork is made **Public** for marking. Answers should be added to the # INSERT ANSWERS HERE # section above in the **README.md** file of your forked repository.

Questions 1, 2 and 3 should be answered in the **README.md** file of the `logistic_growth` repo that you forked during the practical. To answer those questions here, simply include a link to your logistic_growth repo.

**Submission**: Please submit a single **PDF** file with your candidate number (and no other identifying information), and a link to your fork of the `reproducible-research_homework` repo with the completed answers. All answers should be on the `main` branch.

## Assignment questions 

1) (**10 points**) Annotate the **README.md** file in your `logistic_growth` repo with more detailed information about the analysis. Add a section on the results and include the estimates for $N_0$, $r$ and $K$ (mention which *.csv file you used).
   
2) (**10 points**) Use your estimates of $N_0$ and $r$ to calculate the population size at $t$ = 4980 min, assuming that the population grows exponentially. How does it compare to the population size predicted under logistic growth? 

3) (**20 points**) Add an R script to your repository that makes a graph comparing the exponential and logistic growth curves (using the same parameter estimates you found). Upload this graph to your repo and include it in the **README.md** file so it can be viewed in the repo homepage.
   
4) (**30 points**) Sometimes we are interested in modelling a process that involves randomness. A good example is Brownian motion. We will explore how to simulate a random process in a way that it is reproducible:

   - A script for simulating a random_walk is provided in the `question-4-code` folder of this repo. Execute the code to produce the paths of two random walks. What do you observe? (10 points)
   - Investigate the term **random seeds**. What is a random seed and how does it work? (5 points)
   - Edit the script to make a reproducible simulation of Brownian motion. Commit the file and push it to your forked `reproducible-research_homework` repo. (10 points)
   - Go to your commit history and click on the latest commit. Show the edit you made to the code in the comparison view (add this image to the **README.md** of the fork). (5 points)

5) (**30 points**) In 2014, Cui, Schlub and Holmes published an article in the *Journal of Virology* (doi: https://doi.org/10.1128/jvi.00362-14) showing that the size of viral particles, more specifically their volume, could be predicted from their genome size (length). They found that this relationship can be modelled using an allometric equation of the form **$`V = \beta L^{\alpha}`$**, where $`V`$ is the virion volume in nm<sup>3</sup> and $`L`$ is the genome length in nucleotides.

   - Import the data for double-stranded DNA (dsDNA) viruses taken from the Supplementary Materials of the original paper into Posit Cloud (the csv file is in the `question-5-data` folder). How many rows and columns does the table have? (3 points)
   - What transformation can you use to fit a linear model to the data? Apply the transformation. (3 points)
   - Find the exponent ($\alpha$) and scaling factor ($\beta$) of the allometric law for dsDNA viruses and write the p-values from the model you obtained, are they statistically significant? Compare the values you found to those shown in **Table 2** of the paper, did you find the same values? (10 points)
   - Write the code to reproduce the figure shown below. (10 points)

  <p align="center">
     <img src="https://github.com/josegabrielnb/reproducible-research_homework/blob/main/question-5-data/allometric_scaling.png" width="600" height="500">
  </p>

  - What is the estimated volume of a 300 kb dsDNA virus? (4 points)

**Bonus** (**10 points**) Explain the difference between reproducibility and replicability in scientific research. How can git and GitHub be used to enhance the reproducibility and replicability of your work? what limitations do they have? (e.g. check the platform [protocols.io](https://www.protocols.io/)).
