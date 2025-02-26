# Hexagon Muon Detector

Getting started
---------------------------------
Enter the EIC container ([installation instructions](https://github.com/eic/eic-shell)) and go to the directory containing your EIC container (if not already there). 

## Visualizing the Simulation

The Hexagon Muon Detector is a composition of 6 1x8 PCB that is arranged into a hexagon shape totaling 48 readout channels. From the physical structure of hexagons, the expected upper limit of muon path from exact cell position calculations is about 17.32 degrees.

To visualize the xml model, please use 
```
dd_web_display --export hexagon_detector.xml
```
and import the .root file in ([EIC Viewer](https://eic.phy.anl.gov/geoviewer/)) for detail component visualization.

## Running the Simulation

To run, please make sure you are first in the EIC shell environment. After, you can enter the code
```
source setup_env.sh
npsim --compactFile=hexagon_detector.xml -N=100 -G --outputFile=data/tes_output.edm4hep.root --gun.position "0.0 10*cm 10*cm" --gun.momentumMin "4*GeV" --gun.momentumMax "4*GeV" --gun.thetaMin "65*deg" --gun.thetaMax "150*deg" --gun.phiMin "0*deg" --gun.phiMax "360*deg" --gun.distribution "uniform" --gun.particle "mu-"
```
and your simulation results will be in the `\data` folder.

To change the path and name of the output file, change `--outputFile=data/tes_output.edm4hep.root`.
To change the properties of the gun; initial gun position, momentum, gun pointing angle, gun particle, please change the variables starting with `--gun.` to your desire.
To change the number of events, change `-N=`
If you want to generate a `.hepmc` file, please use `gen_particles.cxx` and change the variables `pdgID` and `mass` to your desired particle and run the command
```
root -l -b -q gen_particle.cxx
```
And if you would like to use a `.hepmc` file as an input, please use the following command
```
npsim --compactFile=hexagon_detector.xml -N=100 --inputFiles=input.hepmc
```

## Analysis

To obtain the graph of how well the detector reconstructs angle, please run all of the cells in `AngleAnalysis.ipynb` and checkout the last plot, there are also plot such as angle distribution and multiplicity for simulation checking.
