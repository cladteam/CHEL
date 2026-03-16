# CLAD HEX ENVIRONMENTAL LINKAGE (CHEL)

# Part 1: Scientific and Spatial Foundations

## **1.1 Environmental Health and the Problem of Spatial Representation**

Environmental health research sits at the intersection of spatial processes and population data. The physical phenomena underlying, air pollution, wildfire smoke, extreme heat, hydrologic hazards, industrial contamination, operate continuously across space. Their distribution is governed by atmospheric chemistry, wind velocity, boundary layer dynamics, topography, land cover, hydrology, and infrastructure networks. These processes do not recognize census tracts, ZIP codes, or political districts.

Yet most demographic and health datasets in the United States are reported using administrative geography. Census tracts are constructed to contain roughly equal population counts, not to represent exposure homogeneity. ZIP codes are designed around mail delivery logistics. Counties reflect political and historical demarcations rather than environmental gradients.

This structural mismatch introduces systematic instability into environmental epidemiology. When a rural census tract spans thousands of square kilometers, the environmental heterogeneity within that tract can be extreme. Agricultural emissions, forest canopy, mining operations, water bodies, and transportation corridors may all coexist within the same tract boundary. Aggregating exposure to that tract implicitly assumes spatial homogeneity where none exists.

This is not merely a conceptual concern but formalized in spatial statistics as the Modifiable Areal Unit Problem (MAUP).

---

## **1.2 The Modifiable Areal Unit Problem (MAUP)**

The MAUP describes how statistical relationships change when the units of aggregation change. It has two primary components.

### **1.2.1 Scale Effect**

Statistical estimates differ when data are aggregated at different spatial resolutions. A regression coefficient estimated at tract level will generally differ from the same regression estimated at county level. This divergence arises from aggregation itself, not necessarily from differences in the underlying data-generating process.

### **1.2.2 Zoning Effect**

Even at the same scale, altering the configuration of boundaries changes results. When enumeration zones are redrawn, even without changing their total area, correlation coefficients, regression parameters, and measures of spatial autocorrelation can shift.

Openshaw and Taylor demonstrated that these effects can meaningfully alter inference. Subsequent research in environmental health has shown that area-level analyses of air pollution and respiratory outcomes yield different conclusions when alternate spatial structures are used. Studies examining NO₂ exposure and respiratory morbidity have shown that conclusions about effect presence or absence can depend on the spatial unit of analysis.

The problem is not that aggregation is avoidable, it is that administrative aggregation is arbitrary.

If the spatial unit used for analysis is itself mutable, then inference becomes partially dependent on political geometry rather than environmental reality.

CHEL was designed explicitly to mitigate this instability.

---

## **1.3 Hexagonal Tessellation as Methodological Design**

Rather than rely on census tracts or ZIP codes, CHEL adopts a geometrically uniform, hierarchical hexagonal grid based on Uber’s H3 spatial index.

Hexagons tessellate the plane without gaps and provide isotropic adjacency: the distance between a hexagon’s centroid and each of its six neighbors is identical. This property avoids the directional distortion inherent in square grids, where diagonal neighbors are farther than orthogonal neighbors.

Among tessellating polygons (triangles, squares, hexagons), hexagons minimize perimeter for a given area. Reduced perimeter decreases boundary edge effects and produces smoother spatial gradients. Hexagons better approximate radial diffusion processes such as pollutant spread and heat dispersion.

Resolution selection is equally important. CHEL adopts H3 Resolution 3 (Hex3), in which each cell has an approximate area of 12,000 square kilometers. This resolution was selected deliberately as a balance among:

* Spatial stability across rural and urban regions  
* Protection of participant privacy under HIPAA expert determination  
* Computational feasibility for national-scale datasets  
* Compatibility with tract-based source data

Importantly, H3 is hierarchical. Higher resolutions (Hex4, Hex5) can be generated within the same indexing system, enabling future scale sensitivity analyses without redefining the spatial framework.

Even the U.S. Census Bureau has acknowledged the value of grid-based approaches, citing the temporal stability of gridded data relative to administrative boundaries. Grid cells remain spatially fixed; only their contents change over time. This stability enhances reproducibility.

The choice of a hexagonal grid, therefore, is methodological.

It reflects three core principles:

1. Spatial units should be geometrically uniform.  
2. Spatial units should be independent of population counts.  
3. Spatial units should remain stable over time.

By adopting H3 Hex3, CHEL decouples environmental exposure modeling from administrative geography and reduces MAUP-driven instability.

## **1.4 Rural Geography and the Limits of Administrative Units**

The limitations of administrative geography are particularly acute in rural regions.

Census tracts are constructed to contain roughly similar population counts. In urban areas, this results in geographically compact units. In rural areas, where population density is low, tracts expand dramatically in land area in order to meet minimum population thresholds. A single rural tract may span forests, agricultural land, river basins, industrial facilities, highways, and uninhabited terrain.

Environmental exposure surfaces, however, are rarely homogeneous across such expanses. Agricultural pesticide drift, concentrated animal feeding operations, mining sites, wildland fire burn scars, and prevailing wind corridors introduce localized heterogeneity that tract aggregation obscures.

For social variables, tract-level homogeneity may be a reasonable approximation. For environmental exposures, it is frequently not.

This mismatch becomes even more problematic when privacy constraints prevent the use of tract-level geography altogether. When researchers are limited to ZIP3 or broader units, environmental heterogeneity is further blurred. ZIP codes are not designed around spatial coherence; they are constructed around mail delivery routes. They may be non-contiguous, irregular, and shaped by logistical considerations unrelated to exposure processes.

CHEL’s adoption of a spatially proportional hexagonal grid addresses this limitation directly. Hex3 cells maintain consistent land area regardless of underlying population density. A hex in rural Montana and a hex in urban New York have the same approximate area. This consistency ensures that environmental gradients are represented with equal spatial resolution across the country.

This design choice improves analytic equity between rural and urban research contexts.

---

## **1.5 Empirical Evidence on Grid Effectiveness**

The superiority of hexagonal grids over square grids has been demonstrated in ecological modeling and spatial simulation literature.

Comparative analyses show that:

* Euclidean distance distortion is reduced in hexagonal grids because centroid distances are uniform across all neighboring cells.  
* Hexagons provide more accurate approximations of circular neighborhoods.  
* Hexagonal tessellations minimize edge effects relative to square grids of equal area.  
* Connectivity structures are more consistent, improving adjacency-based modeling.

In contrast, square grids introduce anisotropy because diagonal adjacency differs from orthogonal adjacency. This can affect spatial smoothing algorithms, diffusion modeling, and neighborhood statistics.

Although hexagonal coordinate systems historically posed computational challenges, modern spatial indexing systems such as H3 resolve these constraints by providing globally indexed hierarchical hex grids compatible with standard geospatial libraries.

The growing adoption of hexagonal grids in location intelligence, remote sensing, ecological modeling, and transportation analytics reflects these structural advantages.

---

## **1.6 MAUP in Environmental Health Research**

The MAUP has been demonstrated empirically in environmental health studies.

Investigations of the relationship between NO₂ exposure and respiratory health outcomes in Canada found that ordinary least squares regression results differed significantly when different spatial representations were used. Exploratory spatial analytical methods revealed that scale choice altered correlation strength and sometimes altered conclusions about effect presence.

These findings underscore a critical point: inconsistent results in environmental epidemiology may arise not only from model specification, but from the geometry of the spatial unit itself.

If the spatial unit drives statistical divergence, then reproducibility becomes fragile.

CHEL’s use of a fixed, non-administrative grid reduces zoning-driven instability and allows sensitivity analysis across hierarchical hex levels without redefining boundaries.

---

## **1.7 Downscaling, Spatial Confounding, and Causal Inference**

Beyond MAUP, spatial epidemiology faces additional methodological challenges:

* Spatial confounding between exposure and demographic gradients  
* Misalignment between exposure resolution and outcome resolution  
* Aggregation-induced measurement error  
* Lack of spatial mediation modeling

Research in climate-sensitive exposure analysis has emphasized the need for:

* Bayesian spatial hierarchical models  
* Within-community matched designs  
* Spatially varying effect estimation  
* Downscaling approaches to reconcile coarse health data with finer exposure data

Downscaling methods are common in climate science and remote sensing but underutilized in environmental health.

CHEL’s hex-based architecture creates a foundation for such methods by:

* Providing consistent spatial support across datasets  
* Allowing hierarchical aggregation and disaggregation within the H3 system  
* Supporting future multi-resolution modeling  
* Reducing confounding introduced by mutable boundaries

The choice of Hex3 is about enabling future methodological expansion.

---

## **1.8 Stability Over Time and Reproducibility**

Administrative geographies evolve. Census tracts are periodically redrawn. ZIP codes change as delivery routes shift. Counties may split or merge.

In contrast, H3 grid cells remain spatially fixed. Only their associated data change over time.

This distinction has important implications:

* Temporal comparisons are not confounded by boundary revision.  
* Longitudinal environmental trend analysis is more stable.  
* Cross-year harmonization requires updating inputs, not redefining space.

The U.S. Census Bureau has recognized the value of gridded data for temporal consistency. Grid-based data structures allow researchers to compare like-with-like across time.

CHEL’s use of H3 aligns with this principle of geometric stability.

---

## **1.9 Conceptual Summary of Design Principles**

The scientific foundations of CHEL rest on the following principles:

1. Environmental processes are continuous and rarely align with administrative boundaries.  
2. Administrative geographies introduce MAUP-driven statistical instability.  
3. Hexagonal tessellation reduces directional bias and edge distortion.  
4. Spatial units should be proportional to land area, not population count.  
5. Spatial units should remain stable over time.  
6. Aggregation should be mathematically explicit and reproducible.  
7. Privacy protection must be embedded structurally.

With these principles established, we now move from conceptual framing to data architecture.

# Part 2: Input Infrastructure

## **2.1 Conceptual Overview of the CHEL Data System**

With the spatial framework established, the next question is not how space is represented, but how data enter and move through the system.

CHEL is not a single dataset. It is an integrated geospatial architecture composed of spatial reference layers, environmental exposure datasets, demographic vulnerability measures, health prevalence estimates, climate hazard indicators, and privacy-supporting spatial constructs. These components do not operate independently. They are interdependent stages in a transformation pipeline that culminates in a harmonized hex-level analytical dataset.

Every input entering CHEL follows a defined lineage pathway:

**Source → Cleaning → Spatial Harmonization → Hex Aggregation → Normalization → Module Assignment**

This pathway ensures that the origin, transformation logic, and aggregation assumptions of each variable are explicit and reproducible.

Before examining the aggregation mathematics or spatial linkage pipeline, it is necessary to document the full input architecture on which those operations depend.

---

## **2.2 Foundational Spatial Reference Layers**

The foundation of CHEL is geometric. All subsequent aggregation and linkage operations depend on a set of spatial base layers.

### **2.2.1 H3 Hex3 Grid**

The H3 Resolution 3 grid serves as the analytic backbone of CHEL. Each hexagon is uniquely indexed by a `hex3_id` and its canonical `h3_id`, allowing hierarchical referencing across resolutions. The geometry of each cell is fixed and globally indexed.

Hex3 is the spatial unit at which all environmental, social, health, and climate indicators are ultimately expressed. It is also the geography used for participant linkage after privacy logic is applied.

The hex grid is not modified during processing. It serves as the invariant geometric scaffold of the system.

---

### **2.2.2 ZIP5 and ZIP3 Geometries**

Although CHEL does not aggregate environmental exposures at ZIP level, ZIP geographies play a critical role in the privacy architecture.

Two ZIP5 vintages are used:

* 2019 TIGER ZIP5 geometries

* 2020 TIGER ZIP5 geometries

These correspond to the 2022 and 2024 CHEL releases respectively, ensuring temporal alignment between ZIP boundaries and environmental source datasets.

ZIP3 regions are constructed through a deterministic transformation:

1. Extract the first three digits of each ZIP5 code.  
2. Dissolve all ZIP5 polygons sharing the same three-digit prefix into a unified ZIP3 polygon.

The resulting ZIP3 geometries may consist of multiple disjoint polygon components. These geometries are not used for environmental aggregation. They are used exclusively for:

* Privacy reassignment logic (jitter)  
* Small-cell suppression thresholding  
* ZIP-level participant categorization (in DRC outputs)

Separating environmental aggregation from privacy geography is a deliberate architectural decision. It ensures that exposure modeling is not constrained by privacy boundaries, while still embedding de-identification safeguards downstream.

---

### **2.2.3 State Boundaries**

State geometries are included primarily for contextual classification and validation of spatial joins. They serve as an additional spatial reference for participant linkage and geographic reporting.

---

### **2.2.4 Population Raster (GPW v4)**

The population raster is foundational to CHEL’s privacy logic and sliver construction.

CHEL uses the Gridded Population of the World (GPW v4) raster at 2.5 arc-minute resolution. This raster provides population density per pixel.

Population density alone is insufficient for privacy thresholding. Total population per spatial unit must be derived by converting density to count.

For each raster pixel:

Population\_pixel \= Density\_pixel × Area\_pixel

Pixel area must account for Earth’s curvature. Longitudinal degree length decreases with latitude. The area of a raster pixel centered at latitude φ is approximated by:

Area\_pixel \= R² × Δφ × Δλ × cos(φ)

where:

* R is Earth’s radius  
* Δφ and Δλ are angular resolution increments  
* φ is latitude

This correction prevents systematic overestimation of population at higher latitudes.

The population raster is not directly aggregated to hex in the primary environmental pipeline. Instead, it is used in the construction of ZIP3 × Hex3 intersection “slivers,” which underpin privacy logic.

---

## **2.3 Environmental Burden Inputs**

The environmental burden module integrates multiple data domains, each with distinct native spatial formats.

### **2.3.1 Air Pollution Indicators**

Air pollution indicators include:

* Ozone  
* PM2.5  
* Diesel particulate matter  
* Air toxics cancer risk

These measures are typically modeled and reported at census tract level or fine modeled grids. CHEL harmonizes them by reprojecting to a consistent coordinate system and performing tract-to-hex interpolation using area-weighted aggregation.

These variables capture chronic exposure burdens associated with respiratory and cardiovascular morbidity.

---

### **2.3.2 Hazardous and Industrial Sites**

Hazard proximity indicators include:

* National Priority List (Superfund) sites  
* Toxic Release Inventory (TRI) facilities  
* Treatment, Storage, and Disposal Facilities (TSDFs)  
* Risk Management Plan (RMP) sites  
* Coal and lead mines

These datasets are typically point geometries. CHEL assigns facilities to hexagons using spatial intersection and converts counts to density metrics per hex.

Point-based hazard metrics differ methodologically from tract-based air pollution metrics, but are harmonized at the hex output stage.

---

### **2.3.3 Built Environment and Transportation**

Built environment indicators include:

* Lack of park access  
* Housing built prior to 1980  
* Walkability measures

Transportation infrastructure includes:

* High-volume roads  
* Railways

* Airports

Tract-based variables are interpolated. Line-based and point-based variables are spatially assigned and normalized to hex area.

---

### **2.3.4 Water Pollution**

Impaired surface waters are represented as polygons. CHEL computes intersection proportions between impaired water polygons and hex geometries to derive exposure proxies.

---

## **2.4 Social Vulnerability Inputs**

Social vulnerability indicators derive primarily from American Community Survey 5-year tract estimates. Variables include:

* Poverty (below 200% FPL)  
* Educational attainment  
* Unemployment  
* Renter occupancy  
* Housing cost burden  
* Lack of insurance  
* Lack of internet access  
* Limited English proficiency  
* Disability prevalence  
* Age distribution  
* Group quarters  
* Mobile home prevalence  
* Racial and ethnic minority proportion

These tract-level variables undergo area-weighted interpolation to hex geometry.

---

## **2.5 Health Vulnerability Inputs**

Health prevalence indicators derive from CDC PLACES. Variables include:

* Asthma  
* Coronary heart disease  
* Cancer  
* Diabetes  
* Poor mental health

These measures are estimated at tract level using small-area modeling. CHEL interpolates these to hex geometry and applies national percentile ranking. Tracts in the top tertile for a condition receive a binary flag. The cumulative health vulnerability score is computed as the sum of flags across conditions.

---

## **2.6 Climate Burden Inputs**

Climate hazard indicators include:

* Extreme heat days  
* Wildfire smoke days  
* Wildfire area burned  
* Coastal flooding  
* Riverine flooding  
* Drought  
* Hurricanes  
* Tornadoes  
* Strong wind events

These datasets originate from heterogeneous native units (county, raster, polygon). CHEL harmonizes them to hex geometry using area-weighted or intersection-based aggregation depending on source format.

---

## 2.7 Input Lineage Table

The following table documents the primary spatial, environmental, demographic, and privacy-supporting inputs used in the CHEL pipeline. These datasets form the full upstream dependency graph for aggregation and spatial linkage.

| Input | Native Geometry | Role in CHEL | Source Link |
| ----- | ----- | ----- | ----- |
| H3 Hex3 Grid | Polygon | Primary analytic spatial unit | [https://github.com/uber/h3](https://github.com/uber/h3) |
| EJI 2022 | Census Tract | Environmental burden inputs (2022 release) | [https://www.atsdr.cdc.gov/place-health/php/eji/eji-data-download.html](https://www.atsdr.cdc.gov/place-health/php/eji/eji-data-download.html) |
| EJI 2024 | Census Tract | Environmental burden inputs (2024 release) | [https://www.atsdr.cdc.gov/place-health/php/eji/eji-data-download.html](https://www.atsdr.cdc.gov/place-health/php/eji/eji-data-download.html) |
| ACS NOHSDP | Census Tract | Social vulnerability indicators | [https://www.census.gov/programs-surveys/acs/data.html](https://www.census.gov/programs-surveys/acs/data.html) |
| Population Raster | Raster | Population derivation for slivers and privacy logic | [https://www.earthdata.nasa.gov/data/projects/gpw](https://www.earthdata.nasa.gov/data/projects/gpw) |
| ZIP5 2019 | Polygon | ZIP3 construction (2022 release alignment) | [https://www2.census.gov/geo/tiger/TIGER2019/ZCTA5/](https://www2.census.gov/geo/tiger/TIGER2019/ZCTA5/) |
| ZIP5 2020 | Polygon | ZIP3 construction (2024 release alignment) | [https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2020\&layergroup=ZIP%20Code%20Tabulation%20Areas](https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2020&layergroup=ZIP%20Code%20Tabulation%20Areas) |
| States | Polygon | State-level classification and linkage validation | [https://www2.census.gov/geo/tiger/TIGER2025/STATE/](https://www2.census.gov/geo/tiger/TIGER2025/STATE/) |
| Geocodes | Point | Participant coordinate inputs for spatial linkage | N/A |

# Part 3: Mathematical Aggregation Framework

## **3.1 From Native Geography to Hex Geometry**

The datasets documented in Part II enter CHEL in census tract format through the aggregation of EJI ([Environmental Justice Index](https://www.atsdr.cdc.gov/place-health/php/eji/index.html)) but derive from heterogeneous spatial formats:

* Census tracts (ACS, EJI, CDC PLACES)  
* Raster grids (population density, wildfire smoke)  
* Points (facilities, airports)  
* Lines (roads, rail)  
* Polygons (impaired waters, wildfire burn scars)  
* Participant point locations

The central mathematical task of CHEL is to transform each of these into values defined at the Hex3 spatial unit. Hex3 serves as the common support for all variables. Therefore, every input must be re-expressed in terms of hex geometry.

This requires distinct aggregation strategies depending on the native spatial format of the EJI input datasets.

---

## **3.2 Area-Weighted Interpolation (Tract → Hex)**

Most social and health indicators originate at census tract level. To harmonize these with the hex grid, CHEL uses area-weighted interpolation.

Let:

* $$A\_(t∩h)$$ denote the intersection area between tract t and hex h

* $$A\_h$$ denote the total area of hex $$h$$

* $$X\_t$$ denote the tract-level value

The weight assigned to tract t when computing the value for hex h is:

$$w\_(t,h) \= A\_(t∩h) / A\_h$$

The hex-level value $$X\_h$$ is computed as:

$$X\_h \= SUM over t in T\_h of ( X\_t \* w\_(t,h) )$$

where $$T\_h$$ is the set of tracts intersecting hex $$h$$.

---

### **Why Area Weighting?**

Area-weighting assumes that the tract-level value is spatially homogeneous within tract boundaries. Under that assumption, the portion of a tract contributing to a hex is proportional to the fraction of tract area overlapping the hex.

This is not a perfect assumption. It introduces interpolation bias when:

* Within-tract spatial heterogeneity is large  
* Tracts are very large (especially rural tracts)

However, area-weighting is transparent, reproducible, and does not introduce model-based assumptions about intra-tract distribution.

It is therefore appropriate for:

* Rate-based indicators  
* Modeled exposure estimates  
* Prevalence measures

---

### **Bias Considerations**

Interpolation bias magnitude is proportional to within-tract variance.

If a tract contains two highly distinct subregions, area-weighting will average them proportionally by area, even if population is unevenly distributed within the tract.

This is one reason CHEL uses population-weighted aggregation for count preservation when appropriate.

---

## **3.3 Population-Weighted Aggregation**

For variables representing population totals or counts, preserving total population consistency is essential.

Let:

* $$Pop\_t$$ denote tract population

* $$A\_t$$ denote tract area

The hex-level population is computed as:

$$Pop\_h \= SUM over t in T\_h of ( Pop\_t \* ( A\_(t∩h) / A\_t ) )$$

This formulation ensures that, when all hexes are summed, total population approximates the tract totals.

This method differs from the area-weighted mean because the denominator is A\_t rather than A\_h.

Area-weighted mean distributes tract values proportionally into hex area.

Population-weighted aggregation distributes tract counts proportionally based on fraction of tract area contributing to each hex.

---

## **3.4 Density Metrics for Point and Line Data**

Point-based inputs (e.g., TRI facilities, Superfund sites, RMP facilities) are assigned to hexes using spatial intersection.

If $$Count\_h$$ represents the number of facilities in hex h, density is computed as:

Density\_h \= Count\_h / Area\_h

Because all Hex3 cells have approximately equal area, density normalization primarily ensures consistency in case of minor geometric variation.

Line-based features (e.g., major roads) may be converted to:

* Total line length per hex  
* Line density per square kilometer

Polygon-based hazard features (e.g., impaired waters) are aggregated using intersection area proportion relative to hex area.

---

## **3.5 Raster Aggregation**

Raster inputs require cell-based integration.

For each raster pixel intersecting hex h:

Value\_pixel \= Density\_pixel \* Area\_pixel

Hex-level raster value:

Value\_h \= SUM over pixels intersecting h of ( Value\_pixel )

This method is used for population derivation and can also apply to modeled exposure surfaces when necessary.

---

## **3.6 Percentile Normalization**

To allow comparison across heterogeneous indicators (e.g., PM2.5 vs poverty vs wildfire days), CHEL applies national percentile ranking aggregated from the EJI source. See [EJI technical documentation](https://www.atsdr.cdc.gov/place-health/php/eji/eji-technical-documentation.html) for details on rank calculation.

Let:

* Order\_i denote the rank order of hex i among all hexes  
* N denote total number of hexes

Percentile rank:

Rank\_i \= ( Order\_i / N ) \* 100

This places each indicator on a standardized 0–100 scale.

Percentile ranking has two advantages:

1. It reduces sensitivity to extreme outliers.  
2. It allows aggregation of heterogeneous units without unit mismatch.

---

## **3.7 Binary Thresholding for Health Vulnerability**

Health vulnerability is constructed differently from continuous burden metrics.

For each health indicator:

Flag\_i \= 1 if Rank\_i \>= 66.7  
 Flag\_i \= 0 otherwise

The composite health vulnerability score is computed as:

HealthScore\_h \= SUM of flags across conditions

This approach emphasizes cumulative biological susceptibility rather than magnitude of prevalence alone.

---

## **3.8 Composite Index Construction**

In some modules, EJI provides cumulative burden by tract, CHEL aggregates percentile ranks or rank-based scores using:

* Sums of ranks  
* Ranks of summed ranks  
* Threshold multiplication (where appropriate)

Normalization precedes aggregation and derives from the EJI source dataset.

---

## **3.9 Transition to Pipeline Logic**

All of the above aggregation logic assumes that tract, raster, point, and polygon geometries have already been:

* Reprojected into consistent coordinate reference systems  
* Validated for geometric integrity  
* Intersected correctly with hex boundaries

These spatial operations are implemented in the pipeline described in Part IV.

The mathematical definitions in this section define the transformation rules.

Part IV will define the computational workflow that executes them.

---

## **3.10 A Unifying View: Aggregation as a Geometry-Weighted Operator**

All CHEL aggregation can be expressed as a mapping from values defined on a source support to a target support (Hex3). The fundamental distinction across methods is **what is being preserved**:

* **Preserve mean intensity** (e.g., modeled concentration, prevalence) → area-weighted mean  
* **Preserve totals** (e.g., population counts) → area-proportional allocation (a form of mass conservation)  
* **Preserve occurrence intensity** (e.g., facilities) → density or rate per area (or per population where justified)  
* **Preserve areal coverage** (e.g., impaired waters) → fraction of hex area covered or intersected

CHEL uses the simplest transparent operator that is consistent with the semantics of each variable.

This is the key principle: aggregation must match meaning.

---

# Part 4: Quality Assurance, Validation, and Technical Limitations

## **4.1 Purpose and Scope of Validation**

The purpose of validation in CHEL is to confirm that each transformation produces results consistent with both the underlying mathematics and the meaning of the source data.

CHEL performs multiple geometric and statistical operations, including spatial overlays, coordinate reprojections, raster zonal aggregation, tract-to-hex interpolation, density normalization, and deterministic privacy reassignment. Each operation carries assumptions about geometry, scale, and interpretation. If those assumptions are violated, downstream indicators may remain numerically plausible while being conceptually incorrect.

For example:

* Area-based interpolation requires area to be computed in an equal-area projection.

* Population allocation requires consistent tract boundaries and complete spatial coverage.

* Raster aggregation requires correct pixel area estimation as a function of latitude.

* Nearest spatial joins require deterministic tie-breaking and consistent distance metrics.

Validation therefore examines whether:

1. Geometric operations preserve expected spatial relationships.

2. Aggregation preserves conservation properties where required.

3. Derived values fall within mathematically valid ranges.

4. Output patterns are consistent with known characteristics of the source datasets.

These checks are implemented at each stage of the pipeline rather than as a single terminal review. The objective is to ensure that the computational implementation faithfully executes the aggregation framework defined in Part III and the linkage logic defined in Part IV.

## **4.2 Geometric Validation**

### **4.2.1 Coordinate Reference Systems**

All area-based calculations in CHEL depend on correct projection. Area must be computed in an equal-area coordinate reference system. Calculating polygon area in geographic coordinates (latitude/longitude degrees) introduces distortion that increases with latitude.

Before performing:

* Tract-to-hex intersections

* ZIP3 × Hex3 overlays

* Polygon coverage calculations

* Sliver construction

all geometries are reprojected into a consistent equal-area CRS (e.g., EPSG:5070). Validation confirms:

* All input layers share the same CRS before overlay.

* No unintended reprojection occurs during intermediate processing.

* Area calculations are performed only after reprojection.

Failure at this stage would systematically bias every area-weighted aggregation described in Part III.

---

### **4.2.2 Geometry Integrity**

Spatial overlays assume valid polygon geometries. Self-intersections, zero-area artifacts, or corrupted rings can produce spurious intersection fragments.

Before aggregation, geometry checks include:

* Validity testing for each feature.

* Repair of minor topology errors where possible.

* Removal or logging of irreparable geometries.

After overlay operations (e.g., sliver construction), additional checks confirm:

* No duplicate (ZIP3, Hex3) sliver pairs exist.

* Sliver areas are positive and within expected magnitude ranges.

* The sum of sliver areas within a hex approximates the hex’s total area within tolerance.

These checks ensure that overlay logic did not generate artificial fragments or area inflation.

---

## **4.3 Attribute Validation**

### **4.3.1 Conservation Diagnostics**

For variables representing totals (e.g., population), aggregation must approximate conservation.

After tract-to-hex population allocation:

Sum over hexes of Pop\_h ≈ Sum over tracts of Pop\_t

Minor discrepancies may arise from rounding or boundary clipping. Large discrepancies indicate:

* Incomplete spatial coverage

* Projection inconsistency

* Overlay misalignment

Conservation checks are therefore treated as structural validation rather than descriptive statistics.

---

### **4.3.2 Range and Domain Checks**

For each derived indicator, validation confirms that values fall within mathematically valid bounds:

* Percentile ranks are constrained to \[0, 100\].

* Binary flags are constrained to {0, 1}.

* Density measures are non-negative.

* Composite scores do not exceed their theoretical maxima.

Indicators falling outside expected ranges are flagged for review.

---

### **4.3.3 Null Handling**

CHEL distinguishes among:

* Structural nulls (no source data available)

* Derived nulls (aggregation impossible due to geometry mismatch)

* True zeros (absence of exposure or event)

Null propagation rules are explicitly defined. For percentile ranking, null values are excluded from ranking denominator N unless otherwise documented. This prevents missing data from being interpreted as minimal exposure.

---

## **4.4 Visual Inspection and Pattern Review**

Quantitative diagnostics are complemented by visual review of spatial outputs.

Maps of hex-level indicators are examined to confirm that:

* Broad spatial gradients align with known environmental patterns.

* Boundaries do not show unnatural discontinuities suggestive of tract artifacts.

* Densities cluster plausibly around known facility locations.

* Coastal and border hexes do not exhibit implausible truncation artifacts.

Visual inspection serves as a qualitative confirmation that aggregation and interpolation behaved as expected.

---

## **4.5 Pipeline Stage Validation**

Validation procedures are applied within each computational stage.

### **4.5.1 Sliver Construction**

Checks include:

* The union of slivers within a ZIP3 approximates ZIP3 area.

* The union of slivers within a hex approximates hex area.

* Sliver population totals are non-negative and plausible relative to ZIP3 totals.

These checks confirm the correctness of overlay and zonal aggregation logic.

---

### **4.5.2 Spatial Linkage**

For participant linkage:

* All points receive deterministic hex assignments.

* Points falling outside any ZIP3 boundary are logged and reviewed.

* Duplicate resolution removes only records matching defined key combinations.

Assignment stability is tested by re-running linkage on identical inputs and confirming identical outputs.

---

## **4.6 Technical Limitations**

CHEL acknowledges several structural limitations.

### **4.6.1 Interpolation Assumptions**

Area-weighted interpolation assumes uniform distribution within tracts. When within-tract heterogeneity is high, hex-level values approximate tract averages rather than local micro-patterns.

### **4.6.2 Raster Resolution**

Population raster resolution limits precision of sliver-level population estimates. Small slivers intersecting few raster cells may exhibit discretization effects.

### **4.6.3 Fixed Grid Alignment**

Hex grids do not conform to natural boundaries such as rivers, watershed divides, or transportation corridors. Environmental processes tied tightly to such features may not align perfectly with hex boundaries.

### **4.6.4 Source Data Uncertainty**

Modeled environmental exposures (e.g., air pollution estimates) contain inherent uncertainty independent of spatial aggregation.

---

## **4.7 Measurement Error and Spatial Misclassification**

Spatial misclassification in CHEL may arise from:

* Tract-to-hex interpolation error

* Raster discretization error

* Privacy reassignment

The magnitude of misclassification depends on:

* Within-tract spatial heterogeneity

* Raster resolution relative to hex size

* Population distribution within ZIP3 boundaries

Sensitivity analyses across alternative hex resolutions provide one approach to assessing robustness.

---

## **4.8 Recommended Analytical Practices**

Users of CHEL are encouraged to:

* Conduct sensitivity analyses using alternative spatial resolutions where feasible.

* Evaluate models with and without jitter-reassigned records.

* Consider spatial autocorrelation structures in regression models.

* Document assumptions about interpolation and normalization when interpreting results.

CHEL provides a stable spatial framework; rigorous inference remains the responsibility of the analyst.

# Part 5: Cross Year Harmonization and Versioning

## **5.1 Rationale for Versioned Releases**

CHEL is designed as a spatial framework rather than a static dataset. Environmental, demographic, and health source data are periodically updated. As a result, CHEL must support versioned releases that reflect updated inputs while preserving methodological consistency.

Two primary releases are currently defined:

* CHEL 2022

* CHEL 2024

Each release corresponds to a specific set of source data vintages and reference geometries.

Versioning allows:

* Incorporation of updated environmental exposure models

* Alignment with updated ACS 5-year estimates

* Alignment with updated ZIP and boundary files

* Preservation of reproducibility within each release

Each CHEL release is internally consistent. Cross-release comparisons require explicit attention to input differences.

---

## **5.2 Stable Elements Across Releases**

Certain components remain methodologically stable between CHEL 2022 and CHEL 2024\.

### **5.2.1 Hexagonal Grid Framework**

The H3 hierarchical indexing system remains constant. Resolution 3 (Hex3) continues to serve as the base analytic geography. While the underlying H3 indexing system allows higher resolutions, the aggregation level remains fixed for comparability.

The aggregation formulas defined in Part III are unchanged between releases.

---

### **5.2.2 Aggregation Methodology**

The following remain identical across releases:

* Area-weighted interpolation logic

* Population-weighted allocation logic

* Density normalization methods

* Percentile ranking procedure

* Binary threshold logic for health vulnerability

* Composite scoring strategy

This ensures that differences between releases arise from updated source data, not altered aggregation mathematics.

---

## **5.3 Updated Elements Between 2022 and 2024**

Although aggregation logic remains stable, several inputs differ across releases.

### **5.3.1 Environmental Inputs**

EJI 2022 and EJI 2024 are distinct source datasets. Differences may include:

* Updated modeled air pollution surfaces

* Revised facility inventories

* Updated demographic covariates

* Revised risk scoring methodologies at the source level

These differences propagate through tract-to-hex interpolation but do not alter the transformation method.

---

### **5.3.2 ACS Data Vintages**

ACS 5-year estimates used in each release correspond to different rolling periods. Changes in:

* Poverty rates

* Educational attainment

* Insurance coverage

* Renter prevalence

reflect updated survey estimates rather than methodological changes within CHEL.

---

### **5.3.3 ZIP Boundary Updates**

CHEL 2022 uses ZIP5 geometries aligned with the 2019 TIGER release.  
 CHEL 2024 uses ZIP5 geometries aligned with the 2020 TIGER release.

ZIP3 regions derived from these vintages may differ slightly in geometry. Because ZIP3 is used in privacy logic, these differences may affect sliver population calculations and, in rare cases, jitter reassignment.

However, these updates do not affect environmental aggregation, which is performed solely at hex level.

---

### **5.3.4 Facility and Hazard Inventories**

Hazard datasets (e.g., TRI, RMP, Superfund) are periodically updated. Facility openings, closures, or reclassifications will affect counts and densities in updated releases.

Again, the transformation logic remains constant; only source counts change.

---

## **5.4 Implications for Longitudinal Analysis**

When comparing CHEL 2022 and CHEL 2024:

* Differences in indicator values may reflect real environmental or demographic change.

* Differences may reflect updated modeling at the source dataset level.

* Differences in privacy reassignment may arise due to updated ZIP boundaries or population changes.

Researchers conducting longitudinal analysis should:

* Confirm that the same indicator definitions are used in both releases.

* Document source dataset vintages explicitly.

* Avoid interpreting small changes without considering input updates.

The stability of hex geometry and aggregation mathematics ensures that observed changes are not artifacts of spatial unit redefinition.

---

## **5.5 Version Documentation and Reproducibility**

Each CHEL release should document:

* Source dataset names and vintages

* Foundry dataset references (RID)

* Projection specifications

* Aggregation method references

* Privacy threshold specification

This documentation enables:

* Reproduction of a specific release

* Audit of transformation logic

* Cross-release traceability

Version control is treated as part of methodological integrity rather than administrative bookkeeping.

---

## **5.6 Summary of Harmonization Strategy**

Cross-year harmonization in CHEL is achieved by holding constant:

* Spatial unit (Hex3)

* Aggregation formulas

* Normalization procedures

* Privacy logic

while allowing:

* Source datasets to update

* ZIP boundaries to align with release year

* Environmental models to reflect updated science

This approach preserves internal consistency while accommodating evolving data landscapes.

