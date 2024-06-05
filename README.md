# Disasters Charter Extension Specification

- **Title:** Disasters Charter
- **Identifier:** <https://terradue.github.io/stac-extensions-disaster/v1.1.0/schema.json>
- **Field Name Prefix:** disaster
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @emmanuelmathot

This document explains the Disasters Charter Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

![The International Charter Space and Major Disasters](images/charter_logo.png)

[The International Charter Space and Major Disasters](https://disasterscharter.org) is a non-binding
charter which provides for the charitable and humanitarian acquisition and transmission of satellite
data to relief organizations in the event of major disasters.

This extension provides with:

- Additional fields for common disaster properties such as type (e.g. cyclone, earthquake, flooding...).
- Additional fields for specific metadata for the charter such as the call or activation identifier.
- Best practises to describe several objects used in the Disasters Charter (Activation, Disaster Area, Acquisition...).

The extension is used in the [Charter Processing Environment](https://cpe.disasterscharter.org) project to catalog all the objects.

- Examples:
  - [Activation example](examples/activation.json): Shows the usage of the extension to describe an [Activation.](#activation) Item.
  - [Acquisition example](examples/acquisition.json): Shows the usage of the extension to describe an [Acquisition](#acquisition) Item.
  - [Call Collection example](examples/call-collection.json): Shows the usage of the extension to describe a [Call](#call) Collection.
  - [Area example](examples/area.json): Shows the usage of the extension to describe an [Area](#area) Item.
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Glossary

This introductory section gives basic defintion of the terms used in the Disasters Charter and thus in this extension. 
More information about [How the Charter works](https://disasterscharter.org/web/guest/how-the-charter-works).

### Activation

An **Activation** represents a Disaster event for which the Charter has been activated.
An identifier is issued or recycled to be associated with a [Call](#call) identifier.
An **Activation** can be therefore linked to one or several [Call(s)](#call).

### Call

When an authorized User submits a request to mobilise the space and associated ground resources
associated with the Charter members in order to obtain data and information on a major disaster,
A new **Call** is issued. It is associated to a new or existing [Activation](#activation).
All related [Acquisitions](#acquisition) shall be associated to the **Call**, not directly the Activation.

### Area

Regions that are affected by the disaster and identified by the parties involved in the Charter process.

### Acquisition

Acquisition represents a satellite resource provided an Agency in the context of the Disaster.
It can be an archived product or a planned acquisition.
Each Acquisition records is associated to a [Call](#call).

### Value Added Product

The Value Added Providers take the data provided by member agencies and interpret this,
assessing what they see from the satellites and compiling it into **Value Added Products**.

## Item Properties and Collection Fields

## Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [x] Links

| Field Name                 | Type      | Description                                                                                                      |
| -------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------- |
| disaster:class             | string    | **REQUIRED**. Identifier of the object described in the item or collection                                       |
| disaster:call_ids          | \[int]    | Identifiers of the related [Call(s)](#call)                                                                      |
| disaster:activation_id     | int       | Identifier of the related [Activation](#activation)                                                              |
| disaster:types             | \[string] | Disaster Types (one of the [category](#disastertypes))                                                           |
| disaster:country           | string    | Related Country identifier based on the ISO-3166 standard. In particular, the Alpha-3 representation. (e.g. BEL) |
| disaster:regions           | \[string] | Free text list identifying regions                                                                               |
| disaster:activation_status | string    | Activation status. One of `open`, `closed`, `archived`.                                                          |
| disaster:resolution_class  | string    | For Class `acquisition`, One of `VLR`, `LR`, `MR`, `HR`, `VHR`                                                   |

### Additional Field Information

#### disaster:types

The `disaster:types` is the commonly used category name to classify the type of disaster.
Here is the list of accepted types:

| Disaster Type     | Description                                                                                                                                                                                                                                                                                                      |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cyclone`         | Tropical [cyclones](https://disasterscharter.org/web/guest/disaster-types/-/article/cyclones) are weather phenomena which form over the Indian and south Pacific Oceans ocean through the release of energy generated by evaporation and saturation of water on the ocean's surface.                             |
| `earthquake`      | [Earthquakes](https://disasterscharter.org/web/guest/disaster-types/-/article/earthquakes) occur following the release of energy when tectonic plates move apart. These plates move in currents in the Earth's lithosphere and the edges, which have been mapped to fault lines, sometimes collide.              |
| `fire`            | [Wildfires](https://disasterscharter.org/web/guest/disaster-types/-/article/fires) occur when vegetated areas are set alight and are particularly common during hot and dry periods. They can occur in forests, grasslands, brush and deserts, and with sufficient wind can rapidly spread.                      |
| `flood`           | Large [Flooding](https://disasterscharter.org/web/guest/disaster-types/-/article/floods) occurs when bodies of water flow onto land that is normally dry.                                                                                                                                                        |
| `ice`             | [Ice](https://disasterscharter.org/web/guest/disaster-types/-/article/ice) on the surface of water or in compacted snow makes for treacherous conditions and can result in injuries if people slip and fall. Water sources may freeze, cutting off access for residents to clean water or heat.                  |
| `snow_hazard`     | [Snow Hazard](https://disasterscharter.org/web/guest/disaster-types/-/article/ice) occurs when temperatures drop below the freezing point, and there is sufficient water in clouds. Snow storms can quickly cause disruption to inhabited areas if the ground temperature is cold enough for the snow to settle. |
| `tsunami`         | Tsunamis are seismic [sea waves](https://disasterscharter.org/web/guest/disaster-types/-/article/ocean-wave) and typically occur as a result of underwater earthquakes or volcanic eruptions.                                                                                                                    |
| `landslide`       | [Landslides](https://disasterscharter.org/web/guest/disaster-types/-/article/landslides) occur when ground on slopes becomes unstable. The unstable ground collapses and flows down the side of a hill or mountain, and can consist of earth, rocks, mud and any debris which may be caught in its wake.         |
| `storm_hurricane` | Tropical [cyclones](https://disasterscharter.org/web/guest/disaster-types/-/article/cyclones) are weather phenomena which form over the Atlantic and northeast Pacific Oceans through the release of energy generated by evaporation and saturation of water on the ocean's surface.                             |
| `oil_spill`       | [Oil spills](https://disasterscharter.org/web/guest/disaster-types/-/article/oil-spills) occur when petroleum oil is released into the ocean following accidents, such as vessels crashing or damage and problems with oil platforms and drilling.                                                               |
| `volcano`         | [Volcanoes](https://disasterscharter.org/web/guest/disaster-types/-/article/volcanoes) are points in the Earth's crust which have ruptured, allowing lava, ash, rocks and gas to erupt during periods of seismic activity.                                                                                       |
| `explosive_event` | [Explosive Events](https://disasterscharter.org/web/guest/disaster-types/-/article/explosive-events) are sudden and violent releases of energy, which can be caused by a number of factors, including human error, natural disasters, or deliberate acts.                                                        |
| `other`           | In addition to the most common forms of natural disasters, there are [other types](https://disasterscharter.org/web/guest/disaster-types/-/article/other) of disasters which may benefit from satellite observations.                                                                                            |

> \[!IMPORTANT]
>
> Some previously applicable types have been deprecated and must be replaced by the new ones:
>
> - `flood_large` and `flash_flood` are **deprecated** and must be replaced by `flood`.
> - `storm_hurricane_rural` and `storm_hurricane_urban` are **deprecated** and must be replaced by `storm_hurricane`.
>

#### disaster:class

The `disaster:class` is the commonly used category name to classify the object described in the item or collection.
Here is the list of suggested types:

- `activation` : [Activation](#activation)
- `area` : [Area](#area)
- `acquisition` : [Acquisition](#acquisition)
- `vap` : [Value Added Product](#value-added-product)

#### disaster:resolution_class

The `disaster:resolution_class` is category code to classify the resolution of the `acquisition` item.

- `VLR` : Very Low Resolution
- `LR` : Low Resolution
- `MR` : Medium Resolution
- `HR` : High Resolution
- `VHR` : Very High Resolution

This nomenclature is proper to the [Disasters Charter](https://disasterscharter.org)
and is used to classify the resolution of the satellite.

### Other Extensions and Specifications

This extension uses and requires additional fields from other specifications or extensions.

The following specifications are relevant here:

- [STAC Common Metadata](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md)
- [STAC SAT Extension](https://github.com/stac-extensions/sat)

| Field Name     | Type       | Description                                                                            |
| -------------- | ---------- | -------------------------------------------------------------------------------------- |
| platform       | string     | Globally unique satellite identifier as defined in common metadata.                    |
| instruments    | \[string\] | The instrument identifier as defined in common metadata.                               |
| datetime       | string     | **REQUIRED**. The disaster or acquisition time As defined in common metadata and STAC. |
| gsd            | number     | Ground sample distance as defined in common metadata.                                  |
| sensor_type    | string     | The sensor type. One of `optical` or `radar`                                           |
| eo:cloud_cover | number     | Cloud cover as defined in the EO extension.                                            |

**Additional REQUIRED fields according to the `disaster:class`:**

| Field Name     | activation | area | acquisition         | vap                 |
| -------------- | ---------- | ---- | ------------------- | ------------------- |
| platform       |            |      | X                   | X (when applicable) |
| instruments    |            |      | X                   | X (when applicable) |
| gsd            |            |      | X                   | X (when applicable) |
| sensor_type    |            |      | X                   | X (when applicable) |
| eo:cloud_cover |            |      | X (when applicable) | X (when applicable) |

## Relation types

The following types should be used as applicable `rel` types in the
[Link Object](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#link-object).

| Type         | Description                                                                                                                                           |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| about        | This link points to the disasterscharter.org page of the disaster                                                                                     |
| area         | This link points to an area Item from an activation Item.                                                                                             |
| derived_from | This link should be used in all [Value Added Product](#value-added-product) to identify one or more [Acquisition(s)](#acquisition) used to create it. |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
