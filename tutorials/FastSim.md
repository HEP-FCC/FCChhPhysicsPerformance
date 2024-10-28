In this tutorial you will learn how to use the common `key4hep` tools for fast, parametrized detector simulation with `Delphes`. We will use the FCC-hh baseline detector scenario and run on Higgs pair production events. We assume that the actual event generation step is already done, and so we will start from existing Les Houches Event (LHE) files. We will then use `Pythia` for the hadronization & particle decays, and `Delphes` for the detector simulation, resulting in `EDM4HEP` "reco"-level events. 

You will get an overview of how the parametrized detector response simulation works, as well as of the `EDM4HEP` event data model. 

In the second part of the tutorial, we will make some simple plots from the `EDM4HEP` we produced. 

# Fast simulation with k4SimDelphes starting from existing LHE files

<!-- In an optional part of the tutorial, you can take a look at how to use the EventProducer framework, which makes use of the core key4hep utilities and provides input/output-handling to run full official productions for FCC studies. This framework can also be used to produce the LHE files, e.g. from existing gridpacks. To run this, you need access to CERN resources. -->

<!-- Methods how to analyse the produced EDM4HEP events are covered in the second part of this tutorial using the FCCAnalyses framework (LINK) and in the previous tutorial (LINK).   -->

<!-- ## Producing EDM4HEP events from existing LHE files  -->
Check if you have setup the software stack and the `DelphesPythia8_EDM4HEP` executable is available, by running `which DelphesPythia8_EDM4HEP`. If this doesn't return a path like `/cvmfs/sw.hsf.org/key4hep/<somewhere>/DelphesPythia8_EDM4HEP` please follow the instructions [here](https://gitlab.nikhef.nl/ailg/future_particle_colliders_tutorial/-/blob/main/Tutorial3_Geometry_and_visualisation/README.md) (again). 

For the usecase of running Delphes fast simulation to produce `EDM4HEP` files, we only need this executable. But you can check which other Delphes utilities are available in your installation by just using the autocomplete functionality, i.e. typing `Delphes` <tab><tab> - this will show you the whole list. They all interface different modules and run with different input/output formats - the names should give you a clue which ones exactly. As mentioned already `DelphesPythia8_EDM4HEP` interfaces `Delphes` and `Pythia8` and outputs `EDM4HEP` files, rather than using the `Delphes` output file format. Another example is `DelphesSTDHEP_EDM4HEP` which uses `STDHEP` as input file format. Here you can really see the strength of having a common software ecosystem like `key4hep` - the same utility is offered for many specific usecases. 

We can check how to actually run the exectuable in question with the help option, for example:

`DelphesPythia8_EDM4HEP -h`

returns

```
Usage: DelphesPythia8config_file output_config_file pythia_card output_file
config_file - configuration file in Tcl format,
output_config_file - configuration file steering the content of the edm4hep output in Tcl format,
pythia_card - Pythia8 configuration file,
output_file - output file in ROOT format.
```

telling us which input arguments it expects. Let's go through them:

- The `config_file`: This is our Delphes card, which contains the parametrisations of the resolutions and efficiencies for a specific detector concept. We will use the baseline FCC-hh Delphes card. It comes pre-installed with the `key4hep` software stack, and you can find the main card under: `$DELPHES_DIR/cards/FCC/scenarios/FCChh_II.tcl`
There are many other cards, for different (future) colliders and detectors in `$DELPHES_DIR/cards/`, which you can also view in your browser on [on github](https://github.com/delphes/delphes/tree/master/cards). 

- The `output_config_file` file: This file defines which collections we have in our output EDM4HEP output file and what their names are. We will use the standard version which comes with the software stack installation as `$K4SIMDELPHES/edm4hep_output_config.tcl`. 

- The `pythia_card`: As the name says, this is the configuration card for `Pythia`. Here we use the one provided as `PythiaCard/tester_pwp8_pp_hh_5f_hhbbyy.cmd`. It tells `Pythia` to run over the di-Higgs LHE file provided (`LHEInput/lhe_tester_ggHH.lhe`).  

- The `output_file`: This is simply the name of the output file that will be produced, you can pick it freely but remember to explicitly include the `.root` file format ending.

Task: Run the event simulation using the cards and inputs as described above. 

<details>
  <summary>Solution</summary>

  `DelphesPythia8_EDM4HEP $DELPHES_DIR/cards/FCC/scenarios/FCChh_II.tcl $K4SIMDELPHES/edm4hep_output_config.tcl ./PythiaCard/tester_pwp8_pp_hh_5f_hhbbyy.cmd tutorial_output.root` 
  
</details>

You should see `Pythia` starting up and summarizing its settings, for example

``` 
 (...)

*-------  PYTHIA Process Initialization  --------------------------*
 |                                                                  |
 | We collide p+ with p+ at a CM energy of 1.000e+05 GeV            |
 |                                                                  |
 |------------------------------------------------------------------|

 (...)
``` 
and a list of modules that it initialised, such as importantly `Delphes` and all its submodules required by the input card:

``` 
 (...)

** INFO: initializing module  Delphes                  
** INFO: initializing module  ParticlePropagator       
** INFO: initializing module  ChargedHadronTrackingEfficiency
** INFO: initializing module  ElectronTrackingEfficiency
** INFO: initializing module  MuonTrackingEfficiency   
** INFO: initializing module  ChargedHadronMomentumSmearing
** INFO: initializing module  ElectronMomentumSmearing 
** INFO: initializing module  MuonMomentumSmearing

 (...)     

``` 
Then it will process 10 events, which should be quick. Let's first take a step back to understand what we processed here exactly.

Take a look at the `Pythia` card, and find the answers to the following questions:

- Can you find the line where we limit the run to 10 events only? 
-  In block 4 of the `Pythia` card we use the `ResonanceDecayUserHook` plug-in to filter decays for specific final state particles. Which is our desired final state, i.e. which Higgs decays do we allow? 
- Where is the LHE file that we load in `Pythia`? Open it and take a look here also. 
	- With which generator were our input events generated? 
	- How many events are in the LHE file? 
	- From which collision, at which energy, and in which production mode are the Higgs boson pairs produced?


<details>
  <summary>Answers</summary>

	  - l2 of the Pythia card
	  - We are filtering for bbyy decays, so one Higgs boson (PDG ID 25) decays to a pair of b-quarks (PDG ID 5) and the other to two photons (PDG ID 22).
	  - The LHE file is found in LHEInput\lhe_tester_ggHH.lhe.
	  	- POWHEG-BOX-V2, see l3 of the LHE file.
	  	- It contains 10 000 events, see l27 of the LHE file.
  	- The production mode is gluon-gluon fusion, in a proton proton collison at 100 TeV, see l5, l28f and l30f. 

</details>

Next, lets look at the `Delphes` card to see how the fast simulation works. For the FCC-hh scenario, we are modelling a detector layout of an inner tracker, followed by electromagnetic and hadronic calorimenters, as well as a separate muon system, which provides better precision and efficiency on muon measurements than the tracker. Parametrizations in bins of the pseudorapidity &eta; and the transverse momentum pT are used to model the response across the different regions of the detector. Roughly, the fast simulation proceeds in the following main steps:

- We start from all *stable particles*, as in particles that are written out by `Pythia` as outgoing particles, that do not further decay, at generator level. These are the input to the `ParticlePropagator` module, which propagates them through the magnetic field of the inner trackers. Neutral particles are propagated in a straight line, while charged particles are deflected on a heliocoidal trajectory - in each case the trajectory is modelled upto the point where the particle enters the calorimeter. Here, the magnetic field strength and coverage of the field (= radius of the inner tracker) are user-defined properties, that depend on the detector scenario we want to study. 
- Next, *tracks* are created for all charged particles, by assuming a given probability for the track to be reconstructed - i.e. tracking efficiency -, as well as a certain momentum resolution of the track. The parametrizations of the track efficiency and resolution depend on the particle type, e.g. you can find the muon tracking efficiency in the module `MuonTrackingEfficiency` and the corresponding momentum resolution function in the separate file `muonMomentumResolution_II.tcl`. Especially the latter can look quite complicated, so [here is an example](Tutorial2_DELPHES/figures/example_param.png) of how the parametrizations for muons look if you plot them. 
- For simulating the calorimeter response, a segmentation in &eta; and &phi; is given in the `Calorimeter` module, and it is assumed that each particle deposits its energy into one of such segments (then called a tower). This module also specifies which fraction of a particle's energy is deposited in the electromagnetic and hadronic calorimeter. The energy deposits in the electromagnetic and hadronic calorimeters are then smeared independently, following parametrizations in energy and pseudo-rapidity, as defined in the card. 
- *Particle-flow* objects are then built from the tracks and calorimeter towers, forming our physics objects. 
- Jets are then reconstructed from these particle flow objects using the standard algorithms, here we will use the `FastJetFinder04` module which uses the anti-kT algorithm with R=0.4. 
- Flavour tagging efficiencies are applied to the reconstructed jets, again as a function of &eta; and pT, for several *working points*, such as the medium b-tagging working point in module `BTaggingM`. 
- *Identification efficiency* parametrizations are defined for objects of interest such as photons, muons and electrons, for example in the `PhotonEfficiency` module. These efficiencies are applied on top of the tracking efficiencies. Furthermore, for these objects an isolation variable (named `PTRatioMax` in the card) is defined in e.g. `ElectronIsolation`. 
- Last, an *overlap removal* between the reconstructed objects is performed in the `UniqueObjectFinder`. As you can see here we are using isolated photons, electrons and muons and the jets reconstruced by `FastJetFinder04`. 
- The last block of the card, the `TreeWriter` module, shows you which objects are propagated to Delphes output level. Note that this doesn't mean we will have them in our `.root` file that we created above, as there is still one step in our simulation chain, which is the conversion from `Delphes` output to `EDM4HEP` events. 

Questions:
- In which &eta; range are we reconstructing muon tracks?  
- Which fraction of their energy do electrons deposit in the ECal? What about Kaons? 
- What is the minimum pT of a reconstructed jet? 
- What is the flavour tagging efficiency for a b-jet within |&eta;| < 4.0 and a pT of 250 GeV? 
- What is the maximum photon identification efficiency? 

<details>
  <summary>Answers</summary>

	- Muons tracks are reconstructed up to |eta| < 6, l255 of the Delphes card.
	- Electrons deposit 100% of their energy in the ECal, for Kaons it's 30%, l379 and l393f.
	- Jets with pT > 25 GeV are reconstructed, l709.
  	- The b-tagging efficiency in this bin is 83%, l1225.
  	- The maximum photon identification efficiency is in the bin |eta| < 4.0, pT > 10 GeV and it's around 90% (0.95^2), l1009 and l1013.

</details>

Finally, let's take a look at the `edm4hep_output_config.tcl` file. This tells us which `Delphes` objects we want to store in our `EDM4HEP` output and under what name. Can you match the objects here to those in the Delphes card? 

**Task**: Add a new `EDM4HEP` output collection to store the photons before the isolation requirement and the overlap removal and rerun the `DelphesPythia8` step. 

***Optional task***: If you want to create your own file with higher statistics to use for the next part of the tutorial, you can edit the `Pythia` card to use the full LHE statistics. As this takes some time to run, please submit a job for running this to the batch. The job will take at least 40 min, so this step is fully optional, only if you have time. If you are not familiar with submitting to the batch, there are some pointers [here](https://kb.nikhef.nl/ct/Batch_jobs.html).

To wrap up this part of the tutorial, let's take a quick look at the `.root` output file we produced. You can open and inspect as usual. The tree in it is called `events`. It follows the `EDM4HEP` data model. This is a common event data model for future collider experiments, or in other words, a common format convention on what information of each event is stored in the `ROOT` file and how exactly. In detail the format looks like this:  

![edm4hep data model](Tutorial2_DELPHES/figures/edm4hep_diagram.svg)

If you are doing analysis, you will mostly be interested in the `ReconstructedParticle` collection, which contains all objects reconstructed from the detector responses such as tracks and calorimeter clusters, with the `ParticleID` collection telling us the (likely) type of particle. You can take a look at some of the raw distributions here already, to convince yourself that you actually wrote out some events, but in the next part we will use `podio` to plot in a more convenient way. 

*Note: You have produced an `EDM4HEP` file in the previous tutorial on event generation already. How is it different from the new one we produced here?*

# Simple plots with podio

In this part of the tutorial, we will use the `podio` toolkit from the `key4hep` stack to make some simple plots from the `EDM4HEP` file. In a nutshell, `podio` generates the code (i.e. functions to access the values) from reading the event data model definition. If you are interested in the technical details, you can read more about it [here](https://github.com/key4hep/key4hep-tutorials/blob/main/edm4hep_analysis/edm4hep_api_intro.md). 

The event data model of `EDM4HEP` is given in this [`.yaml` file](https://github.com/key4hep/EDM4hep/blob/main/edm4hep.yaml). If you look at the block starting at l455, you can see what information we have available on our `ReconstructedParticle`s. 

With `podio`, we can now read the file, access the tree and do a regular event loop. A template of the code needed for this is given in `plotting/plot_edm4hep_template.py`. 

You can use your own file from the previous step, if you produced it, or you can copy it from `/user/bstapf/Topical_Lectures_March2024/future_particle_colliders_tutorial/Tutorial2_DELPHES/tutorial_output_noIso.root` or download it from [here](https://cernbox.cern.ch/remote.php/dav/public-files/VdUl77hoR6tNcQ9/tutorial_output_noIso.root).

**Task 1** Plot the number of photons and the invariant mass of the first photon pair in the event, myy. You can use `utils.p4(<ReconstructedParticle>)` to retrieve the four momentum of a `ReconstructedParticle`. 

**Task 2** Add also the distribution of number of photons *before* the isolation requirement, using the extra container you added in the previous part of the tutorial. How does it compare to the number of isolated photons? 

Additionally, you can also plot the `IsolationVar` itself, that a cut is made on during the `Delphes` fast simulation. Look into the `EDM4HEP` for the name of this collection, and how you can read the value of this for one photon in the event. Plot it for the isolated, as well as the non-isolated photons. What value did we cut on to define an isolated photon, can you find this back in the `Delphes` card? *Hint: Plotting with logarithmic y-axis is helpful here*. 



<!-- # Analysing the EDM4HEP events with FCCAnalyses 

It is recommned that you run this tutorial on `lxplus` if you have access, or alternatively on `naf`. 


## Getting started
Clone the specific fork and branch of the FCCAnalyses framework that we will use:

`git clone -b fcchh_tutorial https://github.com/bistapf/FCCAnalyses.git`

`cd FCCAnalyses`

### Setup with access to /cvmfs/fcc.cern.ch/
If you are working on lxplus or naf, you should be able to follow the standard instructions to setup the environment and compile as described in the [main readme](https://github.com/bistapf/FCCAnalyses/blob/fcchh_tutorial/README.md):

```
source setup.sh
mkdir build install
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=../install
make install
cd ..
```

### Setup without access to /cvmfs/fcc.cern.ch/
If you cannot load the setup from `/cvmfs/fcc.cern.ch/` from where you are working, you can try mounting it with the instructions in the bottom of this page. Or you can try this alternative setup:

`source /cvmfs/ilc.desy.de/key4hep/setup.sh`.

Then compile the FCCAnalyses code:
``` 
mkdir build install
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=../install
make install
cd ..
```
Note: Do not source the setup.sh that comes with the framework in this case!

And make sure you link to the correct executables:

```
export PATH=$PWD/bin:$PATH
export LD_LIBRARY_PATH=$PWD/install/lib:$LD_LIBRARY_PATH
```

You should now have the `fccanalysis run` command available and it should point to your local version of the framework (check it with `which fccanalysis`).

Move to the specific tutorial area: `cd tutorial/`. 

### Structure of the framework 
The FCCAnalyses framework makes use of RDataframe to allow for fast and multi-threaded analyses of the EDM4HEP events. It consists of C++ libraries found in `/analyzers/dataframe/` which implement all the work, e.g. actually accessing the EDM4HEP event info, for example a lepton's 4-vector, and calculating other kinematic variables from it, such as an invariant mass. More details on how the EDM4HEP file is actually structured and how the reading works can be found in [this readme](https://github.com/HEP-FCC/FCCAnalyses/blob/basicexamples/examples/basics/README.md). Python scripts are then used to run the analysis with the desired input/output, variable definitions and selections.

Generally, an analysis is implemented in the following steps and scripts: 
- The EDM4HEP file is read and converted into a simple ntuple, with only the desired, user defined branches. The python code for this is usually called `analysis.py` or `analysis_stage<number>.py` in case it consists of multiple stages. You can also apply a pre-selection in this step, to slim down large files. 
- The event selection is defined and applied using `analysis_final.py`. In this step the events are also normalized with their cross-sections. The input here is ntuple produced in step 1. 
- Plotting the results of any selection level is done with `analysis_plots.py`. Here the inputs produced in step 2 are used. 

### Understanding the variables available and how to access them 
The heart of the `analysis.py` file is the definition of the `RDFanalysis` class, using RDataframe. In it you define a new branch with 
` rdf_with_new_branch = rdf.Define("<name_of_branch>", "<value_of_branch>")`. As mentioned, the C++ analyzers of the framework provide functions with which to access (or even filter for) certain physical variables. So these are used for getting `<value_of_branch>` in each case. For example with the following code, you define a new RDataframe called `df2` with branches for the number of jets in the event (`n_jets`), as well as the pT and eta of all jets:

```
df2 = df.Define("n_jets",  "FCCAnalyses::ReconstructedParticle::get_n(Jet)")
		.Define("pT_jets",  "FCCAnalyses::ReconstructedParticle::get_pt(Jet)")
		.Define("eta_jets",  "FCCAnalyses::ReconstructedParticle::get_eta(Jet)")
```
Take note of the following:
- The C++ accessor functions are all found in the namespace `FCCAnalyses::<specific_analyzer>`. So for reconstructed particles, you can find the implementation of the functions in `analyzers/dataframe/src/ReconstructedParticle.cc`, or see [here on github](https://github.com/bistapf/FCCAnalyses/blob/fcchh_tutorial/analyzers/dataframe/src/ReconstructedParticle.cc). If you want to access event generator level particles, use the namespace `FCCAnalyses::MCParticle` and see [this file](https://github.com/bistapf/FCCAnalyses/blob/fcchh_tutorial/analyzers/dataframe/src/MCParticle.cc).
- The input they take are the EDM4HEP collections, which are read directly from the file, or previously defined new branches. Some collections such as `Jet` and `MissingET` can be read directly using their name, for `Photon`, `Electron` and `Muon` we need to read them from the `ReconstructedParticle` collections like so:
```
.Alias("Photon0", "Photon#0.index") 
.Define("photons",  "FCCAnalyses::ReconstructedParticle::get(Photon0, ReconstructedParticles)") 
```
then the newly defined `photons` can be used as inputs for the other functions, such as `FCCAnalyses::ReconstructedParticle::get_n()` etc. 
- Most output branches will be a vector branch. For example, `pT_jets` will have multiple entries per event. If you want to access the pT of only the first jet, you have to call it with its index e.g. `pT_jets[0]`. The number of objects per event retrieved with `get_n()` is flat branch. 
- Since we usually do not want to write out everything we have to define (e.g. the `photons` collection), we need to explicitly tell RDataframe which branches to store in the output file, by adding them to a list in the `output()` function of the `RDFanalysis` class. 

If you want to apply some pre-selection at this stage, you can do so with the `Filter` functionality of the RDataframe, for example
```df2 = df2.Filter("n_jets >= 2")```
to write out only events with at least two jets. 

Task: In the previous tutorial, you produced a file of HH(bbyy) events in ED4MHEP format - convince yourself that this file truely contains HH(bbyy) events. You can run the example analysis with `fccanalysis run analysis.py`[^1] - this should help you get started. You can check the branches in the output ntuple interactively in ROOT as normal, the tree in it is called `events`.  If you do not have the file from the previous part, you can download `fastsim_signal_evts.root` from [here](https://cernbox.cern.ch/s/WStQsvCoEqrdNNR). This download link also contains a `mystery_signal.root` of HH events in a different final state, that you could try to identify.  

[^1] Note: Executing this might print some `podio` errors, but it should run nonetheless. 


## Implementing a simple analysis 
While you can apply selection cuts in this first step already, the final selection is usually done with a separate, simpler file, running on the ntuple produced in the previous step. The example provided here is `analysis_final.py` and it can be run with `fccanalysis final analysis_final.py`.

### Normalizing with cross-sections
To normalize each each process to 'real' events, the cross-section is read from a dictionary in a common `.json` file. Currently, it seems that one cannot overwrite the path of the dictionary easily and by default it wants to read from `/cvmfs/fcc.cern.ch/` - if it cannot, it unfortunately fails. If you are working on naf or lxplus, you should hopefully have access here, if not you can try to mounting it specifically with the instructions at the bottom of this page. 

Since we ran on a file that is not in the common dictionary, we need to add it from our analysis config:
```procDictAdd={"<filename>":{"numberOfEvents": <val>, "sumOfWeights": <val>, "crossSection": <val>, "kfactor": <val>, "matchingEfficiency": <val>}}```
If you know the official name of your process (e.g. the bbyy one we produced in the previous part of the tutorial is called `pwp8_pp_hh_lambda100_5f_hhbbaa`), you can find the needed information in the [FCC events database](http://fcc-physics-events.web.cern.ch/fcc-physics-events/FCChh/Delphesevents_fcc_v04.php).

The framework takes care of normalizing with the correct number of events, i.e. it will read that fact that we ran only over 5k events from the metadata of the input file, and the luminosity is applied in the plotting step. 

### Applying an event selection
The selection cuts are then given as a dictionary:
``` 
cutList = {
            "sel0":"<cut_string_1>",
            "sel1":"<cut_string_1> && <cut_string_2>", 
            [..]
            }
```
The cut strings are what you would write in ROOT, and note that the cuts are all applied independently, so if you want to apply `cut1` on top of `cut2` you need to write out the full cut string explicitly. 

In the `histoList` you can then already define the histograms you would like to plot eventually, they will be stored at each step of the selection in a file named `<outname__sel<i>_histo.root`.

With the setting, `doTree = True` additionally the full `events`-tree with all branches as defined in the first step (`analysis.py`) is also written out at each selection level.

### Plotting signal and background 
Finally, one last step is need to make pretty plots: run the plotting with `fccanalysis plots analysis_plots.py`. This file contains all the configuration for the plotting, such as the integrated luminosity to normalize to, output formats, whether to stack signal and backgrounds, axis settings and labels, colours and legends. It uses the histogram file produced by the previous step, at the event selection level(s) specified in `selections`. This unfortunately means that if you want to change the binning of the histograms, you have to go back and edit `analysis_final.py` and rerun this step as well before plotting. 

Task: The example file contains the basic structure and settings, edit it to use your bbyy input file as input. To make a proper plot, we will also need some background events - you can find a file of some yy+jets events [here](https://cernbox.cern.ch/s/WStQsvCoEqrdNNR). To be able to use it in your plots, you need to run it through the previous two steps as well again. Implement some cuts to suppress this background, and plot e.g. the invariant mass of the two photons. 



# Additional steps: Mounting the FCC cvmfs
``` 
sudo mkdir -p /cvmfs/fcc.cern.ch/
sudo mount -t cvmfs fcc.cern.ch /cvmfs/fcc.cern.ch/
```

 -->

<!-- Probably nobody has access to this -->
<!-- ## Optional: Using the EventProducer framework 

The [EventProducer framework](https://github.com/bistapf/EventProducer) simplifies the generation/simulation of events on a large scale, by providing all the input/output handling for many inputs. To be able to use this framework, you need access rights to the dedicated `eos`-area. Check if you can access this path `/eos/experiment/fcc/hh/generation/` - if not, you need to request access in case you want to run something. 

Just as an example, below are instructions how you would be able to produce LHE files from an existing gridpack: 

If you have a gridpack for the event generation, you can produce LHE events from it in the following steps: 

0. If you have never used this framework to generate events before, you must add yourself to the list of users in `config/users.py`. 

1. Copy your gridpack to the FCChh gridpack eos directory `/eos/experiment/fcc/hh/generation/gridpacks/`. For this example we will use the tester gridpack called `mg_pp_vbf_hh_angela.tar.gz`, which is for VBF HH signal with C2V = 2 (and CV = kl = 1 ). 

2. Add the name of your gridpack to the `gridpacklist` in `config/param_FCChh.py`. For `mg_pp_vbf_hh_angela` this is already done, if you are working on the `fcchh_evtgen_updates` branch. 

3. Run the event generation from your gridpack with the following command:

``` python bin/run.py --FCChh --LHE --send --condor --typelhe gp_mg -p mg_pp_vbf_hh_angela --prodtag fcc_v04 -n 10 -N 1 -q longlunch --detector "" ``` 

This will submit 1 job to generate 10 events from the testergridpack to condor. The logs of this job will be found in `./BatchOutputs/FCC/lhe/mg_pp_vbf_hh_angela` and the output Les Houches files will be in `/eos/experiment/fcc/hh/generation/lhe/mg_pp_vbf_hh_angela`.  -->

## Further reading

- Delphes: [Workbook](https://cp3.irmp.ucl.ac.be/projects/delphes) | [Paper](https://link.springer.com/article/10.1007/JHEP02(2014)057) | [Overview](https://www.tcm.phy.cam.ac.uk/~mjh261/pdfs/delphes.pdf)

- [Pythia](https://pythia.org/)

