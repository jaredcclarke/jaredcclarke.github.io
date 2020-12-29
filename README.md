# Belly Button Diversity
## Overview
Roza is searching for the bacteria that produces a protein that can closely resembke the taste of meat. She hypothesized that this bacteria could possibly be located in the human belly button.So with the help of human subjects, Roza has collected and vizualized the top 10 differetn species of bacteria located inbelly buttons for each test subject, along with the frequency that each subject washed their belly button.
### Resources/Tools
* JavaScript
* Google Chrome Version 87.0.4280.88 
* Plotly
* samples.json
* HTML/CSS
* Github

## Results
* Created a function to select a specific patient number from a dropdown menu and to pull corresponding data when collected, into specific areas that reference the index.html 
* Created variables otu_ids, otu_labels, and sample_values by filtering them out of the samples.json file to creat the x and y axes for the bar graph and bubble graphs
* Had to filter and parseFloat the wfreq or belly button washing frequency, in order to create a gauge meter.
```
function init() {
  // Grab a reference to the dropdown select element
  var selector = d3.select("#selDataset");

  // Use the list of sample names to populate the select options
  d3.json("samples.json").then((data) => {
    var sampleNames = data.names;

    sampleNames.forEach((sample) => {
      selector
        .append("option")
        .text(sample)
        .property("value", sample);
    });

    // Use the first sample from the list to build the initial plots
    var firstSample = sampleNames[0];
    buildCharts(firstSample);
    buildMetadata(firstSample);
  })} 


// Initialize the dashboard
init();

function optionChanged(newSample) {
  
  // Fetch new data each time a new sample is selected
  buildMetadata(newSample);
  buildCharts(newSample);

  console.log(newSample);
  
};

// Demographics Panel 
function buildMetadata(sample) {
  d3.json("samples.json").then((data) => {
    var metadata = data.metadata;
    // Filter the data for the object with the desired sample number
    var resultArray = metadata.filter(sampleObj => sampleObj.id == sample);
    var result = resultArray[0];
    // Use d3 to select the panel with id of `#sample-metadata`
    var PANEL = d3.select("#sample-metadata");

    // Use `.html("") to clear any existing metadata
    PANEL.html("");

    // Use `Object.entries` to add each key and value pair to the panel
    // Hint: Inside the loop, you will need to use d3 to append new
    // tags for each key-value in the metadata.
    Object.entries(result).forEach(([key, value]) => {
      PANEL.append("h6").text(`${key.toUpperCase()}: ${value}`);
    });

  });
}

// 1. Create the buildCharts function.
function buildCharts(sample) {
  // 2. Use d3.json to load and retrieve the samples.json file 
  d3.json("samples.json").then((data) => {
    // 3. Create a variable that holds the samples array. 
    var samples = data.samples;
    // 4. Create a variable that filters the samples for the object with the desired sample number.
    var resultsArray = samples.filter(sampleObj => sampleObj.id == sample)
    //  5. Create a variable that holds the first sample in the array.
    var sampleResults = resultsArray[0]



    // 6. Create variables that hold the otu_ids, otu_labels, and sample_values.
    var otu_ids = sampleResults.otu_ids 
    var otu_labels = sampleResults.otu_labels
    var sample_values = sampleResults.sample_values
```

![](https://github.com/jaredcclarke/jaredcclarke.github.io/blob/master/Resources/Screen%20Shot%202020-12-28%20at%2011.20.22%20PM.png)
    
![](https://github.com/jaredcclarke/jaredcclarke.github.io/blob/master/Resources/Screen%20Shot%202020-12-28%20at%2011.20.29%20PM.png)

![](https://github.com/jaredcclarke/jaredcclarke.github.io/blob/master/Resources/Screen%20Shot%202020-12-29%20at%2012.49.30%20AM.png)




