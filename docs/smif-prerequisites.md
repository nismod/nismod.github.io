---
title: Smif prerequisites
layout: page
---

* TOC
{:toc}

## Introduction

The aim of this microsite is to provide advice and guidance for how to prepare your model for the simulation modelling integration framework, [smif](https://github.com/nismod/smif).
This page focusses on practical guidance to help you draw together the various bits and pieces of data, information and configuration you will need.

For technical details on how to use `smif`, please read the [documentation](http://smif.readthedocs.io/en/latest/) for the package.

If you have any questions, comments or suggestions please direct them via e-mail or Slack to the Oxford integration team.

A data template is available to [download](../files/integration_template.xlsx).

## Audience

This document is intended for the following users:

### Data Provider

You collate, summarise and process raw data to produce scenarios of future change, e.g. population, demographics and economic growth.

1. [Scenarios](./smif-prerequisites.html#scenarios)
2. [Metadata](./smif-prerequisites.html#metadata)

### Sector Modeller

You develop and implement a simulation model of an infrastructure system.

1. [Sector Model config](./smif-prerequisites.html#configuration-sector-model)
2. [Interventions](./smif-prerequisites.html#interventions)
3. [Initial Conditions](./smif-prerequisites.html#initial-conditions)
4. [Metadata](./smif-prerequisites.html#metadata)

### System Modeller

You use a system-of-systems model to analyse the evolution of coupled infrastructure systems, interdependencies under different scenarios

1. [Narratives](./smif-prerequisites.html#narratives)

## Packaging and Deployment

The simulation model should be packaged so that it is deployable on the target
machine.

## Wrapping the Model

{% highlight python %}
import example from examples

python_codesnippet = here
{% endhighlight %}

### Error Handling

### Logs

#### Log Level

### Output

## Configuration: Sector Model

The following configuration data is required to integrate a sector model within
the smif framework:

* model name
* path to the wrapper
* name of the wrapper class
* inputs
* outputs
* parameters
* interventions

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| model name | string | `energy_demand` | A unique name
| path | string | `../../models/energy_demand/run.py` | Relative to the project folder |
| classname | string | `EnergyDemandWrapper` | Name of the python class in the wrapper file |
| inputs | list | \<see below\> | |
| outputs | list | \<see below\> | |
| parameters | list | \<see below\> | |
| interventions | string | `energy_demand.yml` | Name of the interventions file in the `project/data/interventions` folder |
| initial conditions | string | `energy_demand_existing.yml` | Name of the file |

### Inputs and Outputs

`smif` requires all model inputs and outputs to be explicitly defined so that data can be passed to and retrieved from a model at runtime.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `population_density` ||
| spatial_resolution | string | `lad` ||
| temporal_resolution | string | `annual` ||
| units | string | `people/km^2`||

The dependency upon another data source are explicitly declared in the integration framework. To declare a dependency, both models must have the requisite inputs and outputs defined.

### Parameters

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `assump_diff_floorarea_pp`| |
| description | string | `Difference in floor area per person in end year compared to base year` | |
| absolute_range | string | (0.5, 2) | |
| suggested_range | string | (0.5, 2) | |
| default_value | string | 1 | |
| units | string | `percentage` | |

## Data Requirements

### Initial Conditions

### Metadata

Anytime that data is specified, an interval and region definition file must be associated with the data. This allows `smif` to perform spatio-temporal conversion operations on the data between models.

#### Intervals

An example interval definition csv file::

```
id,start_hour,end_hour
1,PT0H,PT8760H
```

In the above example, id `1` is associated with the start hour 0 and end hour 8760 - representing the entire year. The ISO8601 standard is used to define hourly intervals.

#### Regions

#### Units

### Interventions

A yml file,

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `nuclear_power_station` ||
| capital_cost_value | float | `20.3` ||
| capital_cost_unit | string | `£B/GW` |
| economic_lifetime | integer | `20` ||
| operational_lifetime | integer | `25` ||
| capacity_value | float | `1000` ||
| capacity_unit | string | `MW` || 
| location | string | `Oxford` ||
| start_year | integer | `2018` ||

### Narratives

An example narratives file::

```
global:
  discount_rate: 0.05
energy_demand:
  assump_diff_floorarea_pp: 0.5
```

### Scenarios

This section is for [data providers](./smif-prerequisites.html#data-provider).

An example scenarios file which shows the change in population for three regions, England, Scotland and Wales for the years 2010, 2015 and 2020.
The polygons associated with the regions are stored in the region definitions file.
The duration associated with the interval 1 are stored in the interval definitions file.

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

The entries in the `timestep` column should be a valid year integer.

The entries in the `region` column should refer to the names of the regions in the associated [region definition file](./smif-prerequisites.html#regions).

The entries in the `interval` column should refer to the id of the intervals in the associated [interval definition file](./smif-prerequisites.html#intervals).

The entries in the `value` column will normally be a floating point number.

The metadata required to define a particular scenario are shown in the table below. It is possible to associate a number of different data sets with the same scenario, so that, for example, choosing the `High Population` scenario allows users to access both population count and density data in the same or different spatial and temporal resolutions.

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `High Population (ONS)` | |
| description | string | `The High ONS Forecast for UK population out to 2050` ||
| scenario_set | string | `population` | |
| parameters | list | \<see below\> | |

For each entry in the scenario parameters list, the following metadata is required:

| Attribute | Type | Example | Notes |
| --- | --- | --- | --- |
| name | string | `density` ||
| spatial_resolution | string | `lad` ||
| temporal_resolution |string | `annual` ||
| units | string | `people/km^2` ||
| filename | string | `population_density_high.csv` ||

