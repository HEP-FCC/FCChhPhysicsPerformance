
## Welcome to the FCC-hh Physics Performance Documentation

### Table of Contents
1. [Organisation](#organisation)
2. [Overview of goals and studies](#overview-of-goals-and-studies)
3. [How to implement your FCC-hh study ](#how-to-implement-your-fcc-hh-study)

-----

### Organisation

#### Meetings and communication 

E-group for the FCC-hh P&P studies: [fcc-ped-hh-physicsperformance-espp25@cern.ch](mailto:fcc-ped-hh-physicsperformance-espp25@cern.ch)

To subscribe, go [here](https://e-groups.cern.ch/e-groups/EgroupsSearchForm.do).

Monthly meetings are planned for Thursdays, 4PM, CERN time, starting from mid October.
- [Indico category](https://indico.cern.ch/category/18814/)

General e-group for FCC-hh studies and input to the European Strategy Update: [fcc-ped-hh-espp25@cern.ch](mailto:fcc-ped-hh-espp25@cern.ch).

Monthly general meetings on Mondays, ~4PM CERN time, starting from 30.09.2024. 
- [Indico category](https://indico.cern.ch/category/18815/)

A kick-off event for the FCC-hh effort was held on 03.09.2024, the [agenda and slides are available here](https://indico.cern.ch/event/1439072/timetable/).

#### Coordinators
- Angela Taliercio (NorthWestern) - angela.taliercio@cern.ch
- Birgit Stapf (CERN) - birgit.stapf@cern.ch
- Sarah Williams (Cambridge) - sarah.louise.williams@cern.ch

Please don't hesitate to reach out to us with any questions or feedback on this documentation. 

<!-- #### Physics Performance meetings -->
<!-- 
O(monthly) meetings: Mondays, 3pm-5pm, CERN time. Usually the third Monday of each month. 
- [indico category "Physics Performance"](https://indico.cern.ch/category/12894/).


E-group used for announcements: **FCC-PED-FeasibilityStudy**.  -->


---------

### Overview of goals and studies

The scope of this platform is to coordinate the effort of updating and extending the physics and performance studies for the proton-proton phase of the Future Circular Collider (FCC-hh), as input for the 2025 review of the European strategy for particle physics. The original [Conceptual Design Report (CDR)](https://link.springer.com/article/10.1140/epjc/s10052-019-6904-3) has clearly established the primary targets and potential of the FCC-hh phase, but new aspects have emerged since then - such as the consideration of different center of mass energy operating points depending on the R&D progress of the required dipple magnets. One clear goal for the strategy update is therefore to review the key benchmark measurement prospects at the FCC-hh under this aspect. Furthermore, there is ample room to contribute physics studies that were not covered by the CDR, or updates of measurement prospects that might benefit from novel analysis techniques or the inclusion of additional channels. On the performance side, the major goal is to move towards a more full simulation approach, especially considering the impact of pile-up, in stand alone studies to solidify the assumptions on detector performance made by the physics studies. 

We have collected a list of ongoing studies as well as ideas of areas below, but other inputs are welcome of course - please get in touch with us if you would like to join the FCC-hh effort with your idea. More explanation can also be found in [these slides](https://indico.cern.ch/event/1439072/contributions/6106999/attachments/2920406/5125885/FCC-hh%20workshop.pdf) from the kick-off meeting. 


#### Ongoing 

- Higgs self-coupling measurement prospects from di-Higgs production rates: Ongoing efforts in updating the projections in the $b\bar{b}\gamma\gamma$ as well as the $b\bar{b}\tau\tau$ channels. Projection for the rarer, more complex $b\bar{b}\ell\ell + E_{T}^{miss}$ is added. 
<!-- - ALPS study? **TBC** -->
- Jet flavour tagging with transformer architecture


#### Planned studies & ideas 
- Single Higgs measurements:
    - Extending $t\bar{t}H$ measurement to the alternate operating scenarios, exploit $t\bar{t}H/t\bar{t}Z$ ratio to constrain $\kappa_t$, 
      use as input to two-dimensional $\kappa_\lambda \, \text{vs} \, \kappa_t$ constraints combining with self-coupling analyses
    - $H(\mu\mu)$ analyses at alternate energy points
    - Analysis of $t\bar{t}H(\gamma\gamma)$ channel previously uncovered
    - Include previously uncovered channels, e.g. $H \rightarrow WW, bb, cc, \tau\tau$. Opportunity to connect with a flavour tagging performance study
  
- Performance studies:
    - More realistic, full simulation tracker studies, e.g. applying ParticleNET, ACTs, including timing information for pile-up suppression, in order to solidify performance benchmarks used by physics studies


----------

### How to implement your FCC-hh study 

#### Overview

 <figure>
  <img src="images/flowchart_fcc_hh_workflow.png" alt="Overview of technical workflow" usemap="#techworkflow">
  <figcaption> <em> Overview of the FCC-hh workflow. Click on the various steps for more information. </em> </figcaption>
</figure> 

<map name="techworkflow">
    <area shape="rect" coords="6,37,279,90" alt="Event generation tutorial for FCC" href="https://hep-fcc.github.io/fcc-tutorials/main/fast-sim-and-analysis/FccFastSimGeneration.html" target="_blank">
    <area shape="rect" coords="286,51,337,73" alt="LHE events database for FCC-hh" href="https://fcc-physics-events.web.cern.ch/FCChh/LHEevents.php" target="_blank">
    <area shape="rect" coords="365,37,607,90" alt="Pythia8" href="https://www.pythia.org/" target="_blank">
    <area shape="rect" coords="637,37,878,90" alt="DELPHES framework for fast simulation of a generic collider experiment" href="https://cp3.irmp.ucl.ac.be/projects/delphes" target="_blank">
    <area shape="rect" coords="705,135,825,155" alt="k4SimDelphes" href="https://github.com/key4hep/k4SimDelphes" target="_blank"> 
    <!-- Alternatively link tutorial> <area shape="rect" coords="705,135,825,155" alt="Tutorial how to use k4SimDelphes" href="https://hep-fcc.github.io/fcc-tutorials/main/fast-sim-and-analysis/k4simdelphes/doc/starterkit/FccFastSimDelphes/Readme.html target="_blank">  -->
    <area shape="rect" coords="640,195,776,220" alt="EDM4hep event data model" href="https://github.com/key4hep/EDM4hep" target="_blank"> 
    <area shape="rect" coords="365,182,607,237" alt="FCCAnalyses framework" href="https://github.com/HEP-FCC/FCCAnalyses" target="_blank"> 
    <area shape="rect" coords="294,197,357,220" alt="ROOT trees information" href="https://root.cern/manual/trees/" target="_blank"> 
    <area shape="rect" coords="6,182,128,237" alt="CMS combine package documentation" href="https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/latest/" target="_blank">
</map>

The typical technical workflow of a FCC-hh study is illustrated above. We rely on the software tools provided by the [key4hep project](https://github.com/key4hep) - a common, turnkey software stack for future colliders. 

Commonly generators like [MadGraph](https://launchpad.net/mg5amcnlo) and [POWHEG](https://powhegbox.mib.infn.it/) are used for the generation of proton-proton collision events at energies ~ 100 TeV. **Info about the PDF sets TBA**. Those events are stored in the [LHE format](https://arxiv.org/abs/hep-ph/0609017). 

Hadronization, particle decays and a fast detector simulation using parametrizations for resolutions and efficiencies with `DELPHES` are applied in one step, resulting in reconstructed events stored in the `EDM4hep` data model. The available `DELPHES` scenarios for FCC-hh and where to find them are described in more detail [below](#delphes-scenarios-for-FCC-hh-and-official-production-campaigns). 

To process the `EDM4hep` events we use the common `FCCAnalyses` framework, providing multi-threaded vectorial analysis tools using `ROOT`'s [RDataframe class](https://root.cern/doc/master/classROOT_1_1RDataFrame.html). 

The output of `FCCAnalyses` framework can either be another (flat) `ROOT` ntuple, or simple histograms, which can be processed further in the standard ways, e.g. with multi-variate analysis (MVA) libraries, and in the final statistical interpretation with the `combine` statistics tool from the `CMS` collaboration. 

More information, as well as hands-on examples for every one of these steps are given in the [Quick Start Example](#quick-start-example) section below. 

#### Delphes scenarios for FCC-hh and official production campaigns

There are two current `DELPHES` cards available for the FCC-hh studies:
- [Scenario I](https://github.com/delphes/delphes/blob/master/cards/FCC/scenarios/FCChh_I.tcl): An optimistic scenario to study benchmarks reaching ultimate precision. Assumes LHC run 2 conditions with e.g. an ideal crystal calorimeter, b-tagging performances slightly better than with current `CMS` best performance with ParticleNet. 
- [Scenario II](https://github.com/delphes/delphes/blob/master/cards/FCC/scenarios/FCChh_II.tcl): This is the **baseline** scenario based on the FCC-hh general purpose detector concept proposed in the CDR. Compared to the previous FCC-hh card used for the first iteration of FCC-hh physics and performance studies for the CDR this implements several bug fixes (e.g. accounting for electron bremsstrahlung, fixes to parametrization issues).

Click below to see more details on the two scenarios. 

<details>
<summary>Comparison table Scenario I and II </summary>
This table compares relative momentum resolutions and efficiencies for a few key physics objects between the two scenarios. Please note that the numbers quoted cover the total range of resolutions and efficiencies, so across all transverse momenta and pseudorapidity bins, including the forward regions up to pseudorapities of 6. 

<table class="tg"><thead>
  <tr>
    <th class="tg-0lax"></th>
    <th class="tg-8d8j" colspan="2"><span style="font-weight:normal">  Relative <em>p</em> resolution</span></th>
    <th class="tg-8d8j" colspan="2"><span style="font-weight:normal">Efficiency</span></th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-7zrl"></td>
    <td class="tg-7zrl">Scenario I</td>
    <td class="tg-7zrl">Scenario II</td>
    <td class="tg-7zrl">Scenario I</td>
    <td class="tg-7zrl">Scenario II</td>
  </tr>
  <tr>
    <td class="tg-7zrl"><span style="font-weight:normal">Electrons</span></td>
    <td class="tg-8d8j"><span style="font-weight:normal">0.4-1%</span></td>
    <td class="tg-8d8j"><span style="font-weight:normal">0.8-3%</span></td>
    <td class="tg-8d8j"><span style="font-weight:normal">76-95%</span></td>
    <td class="tg-8d8j"><span style="font-weight:normal">72-90%</span></td>
  </tr>
  <tr>
    <td class="tg-7zrl"><span style="font-weight:normal">Muons</span></td>
    <td class="tg-8d8j"><span style="font-weight:normal">0.5-3%</span></td>
    <td class="tg-8d8j">1-6%</td>
    <td class="tg-8d8j"><span style="font-weight:normal">90-99%</span></td>
    <td class="tg-8d8j"><span style="font-weight:normal">88-97%</span></td>
  </tr>
  <tr>
    <td class="tg-8d8j" colspan="3">Medium b-tagging </td>
    <td class="tg-8d8j">80-90%</td>
    <td class="tg-8d8j">76-86%</td>
  </tr>
</tbody></table>
</details>

<details>
<summary>Overview of CDR detector concept </summary>
 <figure>
  <img src="images/CDR_detector_concept.png" alt="Overview of technical workflow" >
  <figcaption> <em> Overview of the FCC-hh baseline detector concept as proposed in the CDR. [Slide from M. Selvaggi] </em> </figcaption>
</figure> 
</details>

A database of all large-scale productions of `DELPHES` events for FCC-hh studies can be found [here](https://fcc-physics-events.web.cern.ch/FCChh/index.php). The up-to-date production campaign to use for studies for the 2025 European Strategy update will be using the production tag `v06`. All previous production campaigns are kept for documenation purpose only, click below to see more details. 

<details>
<summary>FCC-hh production tags</summary>

<table class="tg"><thead>
  <tr>
    <th class="tg-7zrl">Production Tag</th>
    <th class="tg-7zrl">Description</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-7zrl">Delphes v0.2</td>
    <td class="tg-0lax">Production for CDR studies, not using EDM4hep yet. Using original baseline DELPHES card (now outdated).</td>
  </tr>
  <tr>
    <td class="tg-7zrl">Delphes v0.3</td>
    <td class="tg-0lax">Production for CDR studies, not using EDM4hep yet. Using original baseline DELPHES card (now outdated).</td>
  </tr>
  <tr>
    <td class="tg-7zrl">Delphes v0.4</td>
    <td class="tg-0lax">First intermediate production switching to EDM4hep. Using original baseline DELPHES card (now outdated).</td>
  </tr>
  <tr>
    <td class="tg-7zrl">Delphes v0.5</td>
    <td class="tg-0lax">Intermediate production using the updated DELPHES scenarios I and II, and pre-release EDM4hep in v0.</td>
  </tr>
  <tr>
    <td class="tg-7zrl">Delphes v0.6</td>
    <td class="tg-0lax">Production for the strategy update 2025 studies - using DELPHES scenarios I and II, and EDM4hep in v1.</td>
  </tr>
</tbody></table>

</details>


You can find the `Delphes` scenarios (and all their needed inputs) in the official [DELPHES git repository](https://github.com/delphes/delphes/blob/master/cards/FCC/scenarios) as well as on `eos` under the path `/eos/experiment/fcc/hh/utils/delphescards/`, where they are sorted into subdirectories corresponding to the respective production tags. 




#### Quick start example 

Click on the steps below to see instructions and examples how to implement them. 

You can also view the slides as well as watch a recording of the hands-on software tutorial covering the first three steps during our first meeting <a href="https://indico.cern.ch/event/1467696/">here</a>.

<details>
  <summary><b>Step 1: LHE availability and generation</b> </summary>
    <br>
    You can find all already generated processes in the LHE database for FCC-hh <a href="https://fcc-physics-events.web.cern.ch/FCChh/LHEevents.php">on this webpage</a>. 
    The database is interactively searchable, and provides all sample generation information such as available statistics and cross-sections. Please contact us with any questions on the samples or if you find missing information or inaccuracies. <br>
    <br>
    All files are available on the FCC-hh <code>eos</code> space under <code>/eos/experiment/fcc/hh/generation/lhe/</code>. 
    <b>To have access to the <code>eos</code> space you must be a member of the <a href ="https://e-groups.cern.ch/e-groups/Egroup.do?egroupId=10164506">fcc-eos-access</a> egroup. Please request membership from the FCC software coordinators.</b> <br>
    <br>
    A (FCC-ee specific) tutorial how to generate your own LHE within the FCC software environment is available <a href="https://hep-fcc.github.io/fcc-tutorials/main/fast-sim-and-analysis/FccFastSimGeneration.html">here</a>. We also run large-scale productions with the <a href="https://github.com/HEP-FCC/EventProducer">EventProducer framework</a>.<br> 
    <br>
    <b>If you require additional LHE generation or would like to add your own production to the database please get in touch so we can arrange that.</b>
</details>

<details>
  <summary><b>Step 2: Fast simulation</b> </summary>
    <br>
    The steps below show a quick example how to produce <code>EDM4hep</code> reco-level samples from existing LHE with <code>Delphes</code> fast simulation, using the FCC-hh cards as explained <a href="#delphes-scenarios-for-fcc-hh-and-official-production-campaigns">above</a>. A more indepth tutorial, explaining the different steps in detail and especially how the fast simulation works conceptually, is available <a href="tutorials/FastSim.md">here</a>. <br>
    <br>
    <b>Ideally this step should be centrally run for large scale productions, relying on the EventProducer framework and making the files available in the database. Please contact us with any production requests.</b> <br>
    <br>
    First we set-up a working directory and the latest <code>key4hep</code> release with the following commands: <br>
    <br>
    <pre><code>
    mkdir EDM4HEP_prod
    cd EDM4HEP_prod
    source /cvmfs/sw.hsf.org/key4hep/setup.sh
    which DelphesPythia8_EDM4HEP
    </code></pre> 
    This should a return a path like <code>/cvmfs/sw.hsf.org/key4hep/_somewhere_/bin/DelphesPythia8_EDM4HEP</code>, which is the tool we will use to run <code>Pythia</code> and <code>Delphes</code> over our LHE events. 
    <br>
    <br>
    Next, we check which input arguments are required for running this with:
    <br>
    <pre><code>
    DelphesPythia8_EDM4HEP -h
    </code></pre> 
    We see that we need to provide the following input files and arguments:
     <ul>
        <li><code>config_file</code>
        - This is the <code>Delphes</code> card, containing the parametrization of efficiencies and resolutions. As explained above, there are currently two available for FCC-hh, with <a href="">Scenario II</a> being the baseline. The <code>key4hep</code> stack that we set up also comes with an installation of <code>Delphes</code>, containing the directory of all available cards in <code>$DELPHES_DIR</code>, so for our example we can use <code>$DELPHES_DIR/cards/FCC/scenarios/FCChh_II.tcl</code>.
        </li>
        <li><code>output_config_file</code>
        - This defines which of the <code>Delphes</code> output collections we want to write to our <code>EDM4hep</code> output file, and with which names. A standard default version of this file also comes with <code>key4hep</code> stack as <code>$K4SIMDELPHES/edm4hep_output_config.tcl</code>.
        </li>
        <li>pythia_card
        - This is the configuration for <code>Pythia</code> that we want to use, specifying which input we want to run over, how many events to process, the hadronization settings and optionally settings for filtering specific particle decay channels and jet matching schemes. For our tutorial we will use the set-up for using a tester di-Higgs production LHE file of 10k events, and filtering that for the final state with two photons and two b-jets, found here: <code>/eos/experiment/fcc/hh/tutorials/lhe_unpacked_tester/tester_pwp8_pp_hh_5f_hhbbyy.cmd</code>. You can find all <code>Pythia</code> cards for officially produced samples in this directory: <code>/eos/experiment/fcc/hh/utils/pythiacards</code>.
        </li>
        <li>output_file
        - Simply the name of the output <code>.root</code> file in <code>EDM4hep</code> format we want to produce. Let's use <code>pwp8_pp_hh_5f_hhbbyy.root</code>. 
        </li>
      </ul> 
    Now you can run everything with:
    <pre><code>
    DelphesPythia8_EDM4HEP $DELPHES_DIR/cards/FCC/scenarios/FCChh_II.tcl $K4SIMDELPHES/edm4hep_output_config.tcl
    /eos/experiment/fcc/hh/tutorials/lhe_unpacked_tester/tester_pwp8_pp_hh_5f_hhbbyy.cmd pwp8_pp_hh_5f_hhbbyy.root  
    </code></pre>
    This will process 10k events, which should take about 30 mins or so, if you are running locally on <code>lxplus</code>.
    In case you want to understand more about how the cards and config files are written, please refer to the <a href="tutorials/FastSim.md">indepth tutorial on fast simulation</a>.
</details>

<details>
  <summary><b>Step 3: Analysis with FCCAnalyses</b> </summary>
    **Describtion to be added**
</details>

<details>
  <summary><b>Step 4: Statistical interpretation with combine</b> </summary>
    <em>To come. Tentatively planned as an interactive tutorial for the second meeting on 14th November 2024. Please let us know if you are interested in this!</em>
</details>

----------
 
### Further resources 

Note: To be checked and updated! 

#### Software tutorials

- the [FCCSW tutorials](https://hep-fcc.github.io/fcc-tutorials/)
- the tutorials given for Snowmass (September 2020) have been recorded, see [here](https://indico.cern.ch/event/945608/timetable/#20200922.detailed) and [here](https://indico.cern.ch/event/949950/timetable/?layout=room#20200929.detailed)
- the extremely useful [FCCSW FORUM page](https://fccsw-forum.web.cern.ch/)


#### Useful repositories
- [FCCSW](https://github.com/HEP-FCC/FCCSW)
- [DELPHES]( https://github.com/delphes/delphes)
- [DD4Hep](https://github.com/AIDASoft/DD4hep)
- [key4hep/EDM4hep](https://github.com/key4hep/EDM4hep)
- [FCCAnalyses](https://github.com/HEP-FCC/FCCAnalyses)



