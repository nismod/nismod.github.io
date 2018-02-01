---
title: Integration checklist
layout: page
---
## Introduction

The aim of this microsite is to provide advice and guidance for how to
prepare your model for the simulation modelling integration framework,
[smif](https://github.com/nismod/smif).
This page focusses on practical guidance to help you draw together
the various bits and pieces of data, information and configuration you will need.

For technical details on how to use `smif`, please read
the [documentation](http://smif.readthedocs.io/en/latest/) for the package.

If you have any questions, comments or suggestions please direct them via
e-mail or Slack to the Oxford integration team.

A data template is available to [download](../files/integration_template.xlsx).

## Follow the right path

Which of these best describes your role within the project?  Click on one of the links to proceed.

* [I develop and implement a simulation model of an infrastructure system](./smif-prerequisites.html#sector-modeller)
* [I collate, summarise and process raw data to produce scenarios of future change](./smif-prerequisites.html#data-provider)
* [I use a system-of-systems model to analyse the evolution of coupled infrastructure systems & interdependencies under different scenarios](./smif-prerequisites.html#system-modeller)

### Sector Modeller

You develop and implement a simulation model of an infrastructure system.

Please follow these guidelines:
1. [Download](../files/integration_template.xlsx) the template
2. Enter [metadata](./smif-prerequisites.html#metadata) into the template
3. Follow the guidelines for [sector model data requirements](./smif-prerequisites.html#sector-model-data-requirements)

### Data Provider

You collate, summarise and process raw data to produce scenarios of
future change, e.g. population, demographics and economic growth.

Please follow the guidelines below to enter information into the template:
1. [Download](../files/integration_template.xlsx) the template
1. Enter [metadata](./smif-prerequisites.html#metadata) into the template
2. Enter [scenario metadata](./smif-prerequisites.html#scenario-definition) into template
2. Enter [scenario](./smif-prerequisites.html#scenarios) data into template or as csvfiles


### System Modeller

You use a system-of-systems model to analyse the evolution of coupled
infrastructure systems, interdependencies under different scenarios

Please follow these guidelines:
1. [Download](../files/integration_template.xlsx) the template
2. Enter [narratives](./smif-prerequisites.html#narratives) into the template

## Contents

* TOC
{:toc}

## Project Data Requirements

### Metadata

This section is for [modellers](./smif-prerequisites.html#sector-modeller) 
and [data providers](./smif-prerequisites.html#data-provider).

> add your data to template tabs `region_definitions`, `interval_definitions`,
  `intervals` and `units`

Anytime that data is specified, a reference to an temporal and spatial resolution must be
associated with each element in the data.

To define temporal resolution, we need an [interval definition](./smif-prerequisites.html#interval-definition).

To define spatial resolution, we need an [region definition](./smif-prerequisites.html#data-provider).

This allows `smif` to perform spatio-temporal conversion operations
on the data between models.

The region and interval definition files allow users to specify the way
in which space and time are divided in their data inputs and outputs.

#### Interval Definition

> add your data to the `interval_definitions` tab in the template

The interval definition relates a unique name to a file containing the interval
data.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `annual` | A unique name for the region definition at project level |
| description | string | `One annual interval of 8760 hours` | |
| filename | string | `annual.csv` | |

#### Intervals

> add your data to the `intervals` tabs in the template*

\*Note that you may need to add multiple intervals tabs if you have many different
  representations of duration in your model

An interval file specifies how the time within a year (comprised of 8760 hours)
is divided into discrete intervals.

An example interval definition csv file::

```
id,start_hour,end_hour
1,PT0H,PT8760H
```

In the above example, id `1` is associated with the start hour 0 and
end hour 8760 - representing the entire year.
The [ISO8601](https://en.wikipedia.org/wiki/ISO_8601#Durations) standard 
is used to define intervals.

This interval id is used in data files to associate a data row with an interval.

#### Region Definition

> add your data to the `region_definitions` tab in the template

Regions can be contained within a shape file or geojson formats,
anything which can be opened by `smif`.
A `name` field should exist in the region file and uniquely identify each region.

![](../fig/maup-lad.png)

This region `name` is then used in data files to associate a data row with an area.

The values for `name` should be unique within the file.
Each shape should be either a polygon or multipolygon.
If a single region has disjoint parts, it should be stored as a multipolygon.

Note that all region definitions within a project should typically refer
to the same total area.
For example, the union of all the region shapes should correspond
to the same outline of the UK, within a UK project.

In addition, region definitions are loaded with the following attributes:

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `lad` | A unique name for the region definition at project level |
| description | string | `Local authority districts for the UK` | |
| filename | string | `lad.shp` | |

#### Units

> add your data to the `units` tab in the template

All SI unit definitions are supported by `smif` (although as of v0.5,
conversion between units is not yet implemented) and are parsed
into a normalised form. For example `MWh` becomes `megawatt_hour`.

In future versions of `smif`, a unit definition file will
allow the specification of conversion functions across units.
`smif` uses a Python package [Pint](http://pint.readthedocs.io/en/latest/index.html) to manage units.

Using Pint, new units and relations between units can be defined
in the following way:
```
hour = 60 * minute = h = hr
minute = 60 * second = min
```

### Narratives

This section is for [system modellers](./smif-prerequisites.html#system-modeller).

Narratives are the means by which packages of assumptions can be included in a
model run. Narratives cut across model parameters, simulation models,
and strategies, enabling complex combinations of user-defined functionality to
be included in a model run.

An example narratives file:

```
global:
  discount_rate: 0.05
energy_demand:
  assump_diff_floorarea_pp: 0.5
```

### Scenario Definition

> add your data to the `scenario_definitions` tab in the template. Add a row for each new scenario.

This section is for [data providers](./smif-prerequisites.html#data-provider).

Scenario definitions hold the metadata associated with the scenario data. 
Add a new row to the scenario definition for each new scenario you add to the template.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `population_count_high` | A unique name |
| description | string | `ONS Population Projection High`| A useful description of the scenario |
| filename | string | `pop_count_high_csv`| The filename or tab name which holds the scenario data |
| spatial_resolution | string | `lad` | The name of the region definition used by the scenario data |
| temporal_resolution | string | `annual` | The name of the interval definition used by the scenario data |
| units | string | `people` | The unit used by the scenario data. Scenario data cannot mix units within a scenario file |

### Scenarios

> add your data to the `scenario` tab in the template or include the data in a csv file. Make a new tab or file for each scenario.

This section is for [data providers](./smif-prerequisites.html#data-provider).

Below is an example scenarios file which shows the change in population
for three regions, England, Scotland and Wales for the years
2010, 2015 and 2020.
The polygons associated with the regions are stored in a [region definitions](./smif-prerequisites.html#region-definition)
file.
The duration associated with the interval `1` are stored
in the [interval definitions](./smif-prerequisites.html#interval-definition) file.
See the [metadata](./smif-prerequisites.html#metadata) section for details on
how to define region and interval definitions if you have not already done so.

```
timestep,region,interval,value
2010,England,1,52000000
2010,Scotland,1,5100000
2010,Wales,1,2900000
2015,England,1,53000000
2015,Scotland,1,5300000
2015,Wales,1,3000000
2020,England,1,54000000
2020,Scotland,1,5500000
2020,Wales,1,3200000
```

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| timestep | integer | `2010` | A valid year integer |
| region | string | `England` | Reference to the names of the regions in the associated [region definition file](./smif-prerequisites.html#regions)|
| interval | string | `1` | Reference to  the id of the intervals in the associated [interval definition file](./smif-prerequisites.html#intervals)|
| value | float | `52000000` | Will normally be a floating point number |

## Sector Model Data Requirements

This section is for [modellers](./smif-prerequisites.html#sector-modeller).

The following configuration data is required to integrate a sector model within
the smif framework

| Attribute | Type | Notes | Template |
| --- | --- | --- | --- |
| inputs | list | [see below](./smif-prerequisites.html#inputs-and-outputs) | Enter data into `sectormodel_inputs` and `input_data` tabs|
| outputs | list | [see below](./smif-prerequisites.html#inputs-and-outputs) | Enter data into `sectormodel_outputs` tab |
| parameters | list | [see below](./smif-prerequisites.html#parameters) | Enter data into `parameters` tab |
| interventions | list | [see below](./smif-prerequisites.html#interventions) | Enter data into `interventions` tab |
| initial conditions | list | [see below](./smif-prerequisites.html#initial-conditions) | Enter data into `initial_conditions` tab |
| initial system | list | [see below](./smif-prerequisites.html#initial-system) | Enter data into `initial_system` tab

### Inputs and Outputs

> add your data to the `sectormodel_inputs`, `sectormodel_outputs` and `data` tabs in the template

`smif` requires all model inputs and outputs to be explicitly defined
so that data can be passed to and retrieved from a model at runtime.

Wherever you have a data passed into your model from another source, you should
define an input (and where that data should come from).
For each of the results your model produces, you need to define an output 
(and where you think that data should go).
For example, a digital communications model may require `population` data from
a scenario as an
input, and produce a `service quality` metric and 
a `fibre-optic repeater electricity demand` as an output both of which are results.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `population_density` | Unique to inputs or outputs |
| spatial_resolution | string | `lad` | Reference to the name of a region definition |
| temporal_resolution | string | `annual` | Reference to the name of an interval definition |
| units | string | `people/km^2`| SI units are automatically parsed, otherwise a warning is raised |
| source/destination notes | string | `population density table, INSERT population_density INTO TABLE population;` | Name and info of the part of the model this data is read from/written to |
| sample/dummy data | string | `population_density` | References the name of an example datafile in the `data` tab |
| absolute_range_lower	| var | `0` | For validation: the lowest value accepted by the model |
| absolute_range_upper	| var | `inf` | For validation: the highest value accepted by the model |
| suggested_range_lower	| var | `set of power stations` | For validation: the lowest value suggested for the model |
| suggested_range_upper	| var | `set of power stations` | For validation: the highest suggested value for the model |
| source	| string | `population scenario` | Where you expect the data will come from e.g. another model or scenario |
| licenses	| string | `open data` | Any notes of data restrictions or licenses to flag follow up |
| url (if applicable)	| string | `http://www.open_pop.org/datasets/2010.html` | A url to the data source if open data and if appropriate |
| description	| string | `Open population density data from the open pop organisation` | A description of the data source |
| tools or script used to process (if applicable)| string | `github.com/nismod/myscript` | A link to the url, name of a script or code or notes used to process the raw data |

The dependencies upon another data source are explicitly declared in the
integration framework.
To declare a dependency, both models must have the requisite inputs
and outputs defined.
For example, if you wish to couple your energy demand model
with an energy supply model, you will need to define outputs
for `electricity demand`, `natural gas demand`, `hydrogen demand` and so on.
The energy supply model would then need to define inputs for `electricity`,
`natural gas` and `hydrogen`.
Note that the names should be unique within a sector model and list of
inputs and outputs.
It is helpful if the names are easy to understand or descriptive.

### Parameters

> add your data to the `parameters` tab in the template

Parameters are the means by which the 'dials and knobs' of a model can be made
visible to `smif`. Once defined, parameters can be modified through the smif GUI
or connected to narratives.

Initially, (as of `smif v0.5`) only floating point parameters are supported,
but future versions will support categorical and boolean parameters.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `assump_diff_floorarea_pp`| |
| description | string | `Difference in floor area per person in end year compared to base year` | |
| absolute_range_lower | var | `0.5` | A value below of this would cause your model to fail |
| absolute_range_upper | var | `inf` | A value above of this would cause your model to fail |
| suggested_range_lower | var | `0.5` | Hints to users as to what is a sensible value |
| suggested_range_upper | var | `2` | Hints to users as to what is a sensible value |
| default_value | float | `1` | |
| units | string | `percentage` | Units should be listed in the `units` tab |

### Interventions

> add your data to the `interventions` tab in the template

This section is for [modellers](./smif-prerequisites.html#sector-modeller).

Interventions represent the lowest level targets of decisions within an
infrastructure simulation model.

To enable the decision module of `smif`, interventions must be defined for each
of the simulation models within a system-of-systems model.

Once defined, these interventions can be exposed to various pieces of functionality
within `smif`, including defining strategies and exploring decision space across
infrastructure system-of-systems.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name* | string | `nuclear_large_oxford` | Unique within a sector model |
| capital_cost_value* | float | `20.3` ||
| capital_cost_unit* | string | `£B` |
| economic_lifetime* | integer | `20` | The duration over which the capital cost is ammortized|
| operational_lifetime | integer | `25` | The duration during which the intervention is active |
| location* | string | `Oxford` | |
| capacity_value | float | `1000` | Example of a custom attribute |
| capacity_unit | string | `MW` | Example of a custom attribute |
| start_year | integer | `2018` | Example of a custom attribute |

*required information

### Initial System

> add your data to the `initial_system` tab in the template

This section is for [modellers](./smif-prerequisites.html#sector-modeller).

These files hold a list of interventions for which the build date is before the
start year of the model time horizon. 
This enables `smif` to construct the initial systems in the simulation models
and users to view, visualise and edit the initial systems in the smif GUI.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| intervention name | string | `sizewell_b` | Reference to the intervention name defined in the interventions file |
| build_year | integer | `1995` | The year in which the historical intervention was comissioned |

### Initial Conditions

> add your data to the `initial_conditions` tab in the template

This section is for [modellers](./smif-prerequisites.html#sector-modeller).

This data holds initialisation values of parameters which are otherwise 
dynamically determined by the model (also called 'state').

For example, the level of a reservoir in a water supply model may be passed
between planning years (an example of inter-seasonal or inter-year storage).
The initial value of the reservoir level can be set in this dataset.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| parameter name | string | `reservoir_level` | Reference to the parameter name defined in the sector model parameters |
| initial value | float | `30294919.123`| The initial value of the paramter |
