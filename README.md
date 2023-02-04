# Data Centers on Wheels: Emissions from Computing Onboard Autonomous Vehicles
## Introduction
This notebook explores the operational carbon emissions from computing onboard autonomous vehicles (AVs) and accompanies the paper, "Data Centers on Wheels: Emissions from Computing Onboard Autonomous Vehicles", published in Jan-Feb 2023 issues of IEEE Micro. Excerpts of the paper are included in the notebook and all reference numbers point to reference numbers in the paper; for more details, please check out our paper. 

While much attention has been paid to data centers’ greenhouse gas emissions, less attention has been paid to autonomous vehicles’ (AVs) potential emissions. In this work, we introduce a framework to probabilistically model the emissions from computing onboard a global fleet of AVs. The framework we present is adaptable to different models of the relevant variables. While we present how we model variables based on our literature survey, you can use the framework to estimate operational emissions for your own parameters for the variables to incorporate new information, different modeling choices, or internal data on variables such as computer power or the workload growth rate.

## Running the notebook
This notebook was developed on a system running Ubuntu 20.04. Set up a conda environment with the correct dependencies from this repository's directory using (replacing `<env>` with choice of environment name):
```
foo@bar:foo$ conda create -n <env> python=3.9
foo@bar:foo$ conda activate <env>
foo@bar:foo$ ./installation.sh
```
Open the notebook using 
```
(<env>) foo@bar:foo$ jupyter notebook ./data_centers_on_wheels_emissions_from_computing_onboard_AVs.ipynb
```
## Updates
We have updated the modeling of future scenarios and make some corrections to the future scenarios in the original paper. The car lifetime would need to be 21 years or 19 years (blue) and 19 years or 16 years (orange) to hit the baselines with the given hardware energy efficiency doubling rates in Figure 4a and 4b respectively. With a constant car lifetime of 12 years under the assumptions in those scenarios, the hardware energy efficiency half life would be 1.7 or 1.9 (blue), and 1.9 or 2.2 (orange) to hit the baselines in Figures 4a and 4b respectively. 

To model a few example future scenarios to show how the framework can be used to model future trends, we make several assumptions including the modeled starting workload and the starting ratio of target hardware energy efficiency to measured hardware energy efficiency in addition to sweeping over future trends in decarbonization, workload growth rate, and hardware energy efficiency growth rate. These assumptions can be changed to model other scenarios of interest and incorporate new information.

One assumption in the future scenarios presented in the paper is that while the computing hardware stays constant over a vehicle's lifetime, the workload continues to increase over the vehicle's lifetime which is handled by simulating an increase in the computer power. We have added a capability to limit this assumption via the `max_workload_growth_factor` variable which controls the maximum amount the workload can increase over a car's lifetime (e.g., a vehicle sold with computing hardware in a specific year may not support the full autonomy workload growth in future years and will only run up to `max_workload_growth_factor` times its starting workload). If this variable is constrained, the emissions can reduce significantly in these scenarios -- we show an example of sweeping through different values of `max_workload_growth_factor` in the notebook. 

In addition, the example scenarios presented in the paper assume that a high simulated computer power can actually be deployed on an AV; given the battery capacity and impact on range, an AV requiring computing power beyond a certain limit is unlikely to be deployed. We have added a capability to limit the simulated computer power via `max_sim_computer_power` that limits the simulated computer power even if the workload size and growth rate requires more (e.g., an AV may not support the full simulated autonomy workload if it requires more computer power than `max_sim_computer_power`). If this variable is constrained, the emissions can reduce significantly in these scenarios -- we show an example of sweeping through different values of `max_sim_computer_power` in the notebook. 

If you reference this work, please cite our paper:
```
@article{sudhakar2022data,
  title={Data Centers on Wheels: Emissions From Computing Onboard Autonomous Vehicles},
  author={Sudhakar, Soumya and Sze, Vivienne and Karaman, Sertac},
  journal={IEEE Micro},
  volume={43},
  number={1},
  pages={29--39},
  year={2022},
  publisher={IEEE}
}
```