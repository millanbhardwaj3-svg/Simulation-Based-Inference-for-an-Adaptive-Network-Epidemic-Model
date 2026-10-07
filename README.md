# Simulation-Based Inference for an Adaptive-Network Epidemic Model

Bayesian parameter inference for a stochastic SIR epidemic on a network that rewires in response to infection, where the likelihood is intractable. Completed with Prof. Alexandre Thiery at the National University of Singapore, March to April 2026.

**Full write-up:** [report.pdf](report.pdf)

## The problem

The epidemic is modelled on a contact network of 200 individuals, starting as an Erdős–Rényi random graph with mean degree around 10 and five initial infections. At each time step, infection spreads along susceptible–infected edges with probability β, infected individuals recover with probability γ, and susceptible individuals cut links to infected neighbours and rewire to a random node with probability ρ. Disease and network therefore evolve together.

I set up inference for θ = (β, γ, ρ) from three observed outputs: the infected fraction over time, the rewiring counts over time and the final degree distribution. The full process is Markov in the network and node states, but the likelihood of the observed summaries requires summing over every possible path of both, so it cannot be computed. Exploratory analysis also showed that recovery and rewiring both suppress spread through different mechanisms, so infection data alone cannot separate them. I used Approximate Bayesian Computation to handle both problems: rejection ABC, regression-adjusted ABC and SMC-ABC.

## Headline results

- With infection summaries alone, the 95% credible interval for ρ covered almost the whole prior, (0.025, 0.783). Designing summaries over the rewiring dynamics narrowed it to (0.178, 0.446), about a third of the prior width.
- Regression-adjusted ABC more than halved the interval again, to (0.232, 0.349), and recovered known parameters on synthetic data.
- SMC-ABC with adaptive proposal kernels reached the same tolerance as rejection ABC using 85,853 simulations instead of 200,000, with an effective sample size of about 1,800 from 2,000 particles.

Full results, figures and robustness checks are in the report.

## Known limitations

- The observed summaries come from the mean trajectory over 40 replicates, while each simulation is a single replicate. For nonlinear summaries like peak height these are not directly comparable.
- Regression-adjusted values were clipped to the prior bounds, which can make intervals look narrower than they are.
- The synthetic recovery check uses a single parameter value and dataset, so it is a sanity check rather than a calibration study.

## Repository contents

| File | Contents |
|---|---|
| `report.pdf` | Full write-up |
| `Main_Analysis.ipynb` | Exploratory analysis, rejection ABC (summary sets A–C), regression adjustment, SMC-ABC |
| `Additional_Analysis.ipynb` | Robustness checks, joint posteriors, posterior predictive checks, synthetic truth recovery |
| `infected_timeseries.csv` | Observed infected fraction (40 replicates) |
| `rewiring_timeseries.csv` | Observed rewiring counts (40 replicates) |
| `final_degree_histograms.csv` | Observed final degree histograms (40 replicates) |

## Running the code

Requires Python 3 with `numpy`, `pandas`, `scipy`, `scikit-learn` and `matplotlib`. Run each notebook top to bottom. The simulator is pure Python, so full runs (100,000 to 200,000 simulations) take several hours.

## Author

Millan Bhardwaj
