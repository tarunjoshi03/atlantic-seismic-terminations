# US Atlantic Margin - Seismic Horizon Tracking & Termination Analysis
### USGS Survey B-06-82-AT | 2D Multichannel Marine Seismic

## What I Built
A Python workflow for automated seismic horizon tracking and termination 
detection on a real 2D marine seismic line from the US Atlantic margin. 
The analysis implements sequence stratigraphy principles (Mitchum, Vail & 
Sangree, 1977) to classify reflector termination types directly from SEGY data.

## Workflow

**1. Data Loading**  
Loaded a post-stack migrated 2D SEGY line (3,195 traces, 7.7 seconds TWT, 
4ms sample rate) from the USGS National Archive of Marine Seismic Surveys 
(NAMSS). Survey B-06-82-AT acquired in 1982 offshore US East Coast.

**2. Seismic Visualization**  
Displayed full seismic section and zoomed into the shelf-slope transition 
zone (traces 400–1800, 800–3500 ms) using industry-standard Red-White-Blue 
colormap.

**3. Automated Horizon Tracking**  
Implemented a waveform similarity tracker using cosine similarity between 
adjacent CDP traces. Seeds a reflector at a user-defined trace/TWT point 
and tracks forward and backward across the line. Parameters: search window 
8 samples, reference half-length 6 samples, minimum similarity 0.4.

Tracked 4 horizons:
- H1 - Seafloor (1,400 traces)
- H2 - Unconformity (721 traces)
- H3 - Mid Sediment Package (535 traces)
- H4 - Deep Reflector (469 traces)

**4. Termination Detection**  
Implemented automated termination classification following Mitchum, Vail & 
Sangree (1977):
- **Onlap** - reflectors terminating upward against a surface
- **Truncation** - reflectors cut from above by erosion
- **Downlap** - prograding reflectors terminating against a base
- **Toplap** - near-flat termination below a surface

Detection uses local dip estimation via linear regression over endpoint 
windows of each horizon pair.

## Key Results
6 termination events detected across 3 horizon pairs:

| ID | Type | Trace | TWT | Horizons |
|----|------|-------|-----|----------|
| T1 | Onlap | 400 | 1122 ms | H1/H2 |
| T2 | Truncation | 1120 | 1196 ms | H1/H2 |
| T3 | Onlap | 442 | 1479 ms | H2/H3 |
| T4 | Truncation | 976 | 1583 ms | H2/H3 |
| T5 | Onlap | 442 | 2194 ms | H3/H4 |
| T6 | Truncation | 868 | 2200 ms | H3/H4 |

The alternating onlap/truncation pattern across the stratigraphic column 
reflects repeated transgressive/regressive cycles on the US Atlantic 
passive margin.

## Results

### Horizon Tracking & Termination Detection
![Termination Analysis](atlantic_terminations_final.png)

### Full Seismic Section
![Full Section](atlantic_seismic_section.png)

## Data Source
USGS National Archive of Marine Seismic Surveys (NAMSS) - Public Domain  
Survey: B-06-82-AT | 2D Multichannel Seismic | US Atlantic Margin | 1982  
Contributor: Bureau of Ocean Energy Management  
https://walrus.wr.usgs.gov/namss/

## References
Mitchum, R.M., Vail, P.R., and Sangree, J.B. (1977). Seismic stratigraphy 
and global changes of sea level, Part 6: Stratigraphic interpretation of 
seismic reflection patterns in depositional sequences. AAPG Memoir 26.

## Tools & Libraries
`Python` `segyio` `numpy` `scipy` `matplotlib`

## Author
**Tarun Joshi** | Petroleum Engineering M.Eng., Texas A&M University  
[LinkedIn](https://www.linkedin.com/in/tarunjoshi03) |
[GitHub](https://github.com/tarunjoshi03)
