# HiClass Code repository 

The code in this repository was written to explore the effect of hidden cladogenesis for SSE models. 
HiSSE allows for cladogenesis with no trait change and requires trait changes to anagenetically along the branches (0A -> 0A, 0A for simplicity this is also referred to in this format: [0A,0A,0A]).
However, this does not allow researchers to ask questions relating to the mode of evolution. ClaSSE allows for trait changes at cladogenetic events but to my knowledge as of April 2025, it has not been implemented with hidden states. To assess if a trait really has an impact on a group's diversification, we ned to compare rates for hidden and empirical states of both anagenetic and cladogenetic transistions. 

![Screen Shot 2025-04-25 at 11 02 40 AM](https://github.com/user-attachments/assets/39a2a060-a7fe-48e5-9e15-824c8db85ace)

As it is written in the revbayes code for the most recent folders (both begining with 05 and 06), there are three main blocks of code describing the allowed anagenetic and cladogenetic transistions. 

<img width="640" alt="Screen Shot 2025-04-25 at 11 11 22 AM" src="https://github.com/user-attachments/assets/59668b6f-7d26-4b82-9599-718d1156edff" />


## Data in this repository
There are seven folders of data that Jenna analyzed between September 2024 and March 2025. These folders have individual code and input files to rerun analyses if needed. The original code came from the GeoHiSSE code produced in McCullough et al. 2022 Sys Bio, which was co-written by Rosana and Jenna in 2020.

Folders 01–03 are on the polyploidy dataset that Jenna ran with a ~600 tip tree. Folder 1 sets the same rate for the cladogenetic events, whereas Folder 2 allows them to be free. However, these analyses did not have the root of the tree set to a particular state. In Folder 3, Jenna set the root to a particular state. After these analyses, Rosana thought that the polyploidy dataset might not be the best dataset in which to test this model. So in Folder 4, Jenna ran the same analysis on a smaller dataset of Restios by Bouchenak-Khelladi and Linder 2017 (~300 tips and different traits). Folder 4 has both the same and different rates for cladogenetic events in different output folders. Rosana heavily edited the code from analysis 4 to make the names for the rates more intuitive, hence analysis 5 on the same tree that Jenna ran again. Rosana also wanted Jenna to try the revised model on a larger tree as well, so she started it on the passerine tree Rosana used for her Sys bio paper on nest type (folder 6). 

Jenna also included some figures that she created for this project as well as the beginings of an introduction in the "00_Figures&Manuscript" folder.  

## Issues with the code 
The code for the "final" analyses for 5 and 6 are flawed. In early March, Rosana realized there was an error in how the mean of the log normal prior is negative. 
We had: 
rate_mean <- ln(ln(num_species/2.0) / observed_phylogeny.rootAge())
that number is negative or very small because  ln(num_species/2.0) / observed_phylogeny.rootAge()=0.2 then log it again you get -1.6 which means that your log-Normal has a negative mean.
This starts off the log normal in values that are not possible for a speciation rate or giving high probabilities to negative values. This was how the code was written in McCullough et al. 2022 and it was fine in that paper because we were specifying log speciations and not speciations directly. 

But there are other issues as well with analyses 5 and 6. If you take the log files for runs 1 and 2 in tracer plot the rates of [0A,0A,0A] and [0A,0A,0B], their marginal densities are a negative correlation which indicates non-identifiability (see screenshot below). Rosana decided that it was time to pause the project because it will take more intense math and time to solve this issue. 
![PNG image](https://github.com/user-attachments/assets/47765c30-9a9f-46e2-810c-961b33923aa6)


