# Schedule optimization

The entire model is developed in SAS as mentioned earlier. 
The given water network features in our modular town :
Source of Water supply (Only 1): Cornwall Water Treatment Plant
Network_Consumers (3 Reticulation Zones): at Ellerslie, Penrose, Newmarket
Network_Valves (2 Valves): Greenwood Valve, EricssonValve
Network_Pumps (2 Pump Stations with 3 pumps in each station): Cornwall_P1, Cornwall_P2, Cornwall_P3, Kingsland_P1, Kingsland_P2, and Kingsland_P3.
Network_Tanks (4 Tanks): at ClearWells, Ellerslie, Penrose, and Newmarket

Conditions given for the above resources and assets:
The Cornwall Water Treatment Plant does not stop production. Its maximum production capacity is at the rate of 3500 m3/h and minimum production capacity is at the rate of 800 m3/h. The rate of flow of water from the source is generally constant. However, we also need to assess the situation if the rate of flow of water changes. We are given the condition that the rate of flow can only change after every 4 hours.
The two valves can be open or closed and we are given the minimum and maximum rate of flow through these valves. However, we also need to assess the condition that if the valve is open, then it must stay open for at least four hours at a constant rate of flow.

|     | Water Source_1 | Valve_Gr  | Valve_Er |
| --- | --- | --- | --- |
| Min rate of flow at m3/h | 800 | 500  | 200  |
| Min rate of flow at m3/h  | 3500  | 1500 | 1000 |
| Constant rate of flow (Hours)  | >=4  | >=4  | >=4 |
| Open (Hours)  | 24  | >=4 | >=4 |
| Close (Hours) | 0   |     |     |

All the 6 pumps are in similar performing condition. They all work at 65% efficiency level. Their lifting capacity is therefore almost similar, except one. All the lifting rates have been provided. A pump can be open or closed. However, we also need to assess the situation if the pump must stay open for at least two hours. 

|     | P1_CrnW | P2_CrnW  | P3_CrnW | P1_KsL | P2_KsL | P3_KsL |
| --- | --- | --- | --- | --- | --- | --- |
| Efficiency | 65% | 65% | 65% | 65% | 65% | 65% |
| Q or Lift Capacity at m3/s  | 600/3600 | 600/3600 | 800/3600 | 800/3600 | 800/3600 | 400/3600 |
| Open (Hours)  | >=2 | >=2 | >=2 | >=2 | >=2 | >=2 |
| Close (Hours) |     |     |     |     |     |     |

All the 4 tanks are cylindrical because we are given a constant cross-sectional area for each tank [3]. They are all top filled and with fixed static head. The initial volume, maximum and minimum volume, the top elevation of each tank is given. 

|     | Tank_CW | Tank_El | Tank_P | Tank_NM |
| --- | --- | --- | --- | --- | 
| Initial Volume in m3 | 29000 | 11000 | 11000 | 17000 |
| Min Volume in m3  | 15000 | 5000 | 5000 | 12000 |
| Max Volume in m3  | 32000 | 14000 | 14000 | 18000 |
| H or Pump Lift (Level of nearest PS-Top level of Tank) | 0 | 90 | -60 | -50 |

Operation cycle is for 24 hours.
There are 3 reticulation zones where demand (consumption) profile at m3/h is given for each hour on a summer weekday. The cost of pumping at the two pumping stations is given. The tariffs rates are given for Off Peak hours, Peak hours and Part Peak hours at the two pump stations for all the six pumps

|     | El Zone | P Zone | NM Zone |
| --- | --- | --- | --- |
| CrnW_T_OP for P1, P2, and P3 | 0.10 |  |  |
| CrnW_T_P for P1, P2, and P3| 0.24 |  |  |
| CrnW_T_PP for P1, P2, and P3  | 0.17 |  |  |
| KsL_T_OP for P1, P2, and P3 |  |  | 0.06 |
| KsL_T_P for P1, P2, and P3 |  |  | 0.18 |
| KsL_T_PP for P1, P2, and P3 |  |  | 0.12 |
| Total Demand for Water in m3/h | 16,188 | 10,821 | 31,036 |

The reticulation zone at New Market (NM Zone) has the maximum demand for water. It can get a supply of water from the NM tank with a top elevation of 200m. The NM tank is the only tank which has two sources. One from the Ericsson Valve at $0 pumping cost (H= 200-250). Another from the Kingsland Pump Station (P1_KsL, P2_KsL, and P3_KsL) at its given tariff rate (H=200-100)
The reticulation zone at Penrose has the minimum demand for water. It gets its supply of water from the Penrose tank with a top elevation of 100m. The Penrose tank gets its supply of water from the Greenwood Valve and there is no pumping cost. 
Considering all the nodes, we can identify eight supply nodes and four demand nodes. There is one origin node, seven transnetwork nodes and four destination nodes.

# Mathematical Formulation

The Decision Variables are number of working hours for Water Source_1, the number of working hours for each of the two valves i.e. Valve_Gr and Valve_Er, the number of working hours for the six pumps i.e. pump schedule [h, np].

The Objective Function is Minimization of Pumping Cost C

Pumping Cost = Energy * Tariff

Energy = Energy used while the pump is running

Energy = [Q * ρ * g * H * time(seconds)]/efficiency * conversion factor

Q = rate of pump flow [m3/s]

ρ = water density, 1000 kg/m3

g = gravity [m/s2], 9.8 m/s2

H = pump lift [m] = pump level to – pump level from

Time = time the pump is running [s], hr * 3600

Efficiency (E) = pump efficiency % =  65%

Conversion factor = 3.6 * 106 J to Kwh

Let K [np] = constant = (Q*ρ*g*H)/E * 3.6 * 106

Min C = K * Network Tariff * Pump Schedule Σ24i=1 h Σ6j=1 np

Where Pump schedule or demand Schedule

np: network pump j, j = 1 to 6

h: hours I, I = 1 to 24

k, nt, , h, np >= 0

Subject to the Constraints:

Network Source rate of flow [ns] * h [hour of flow] > = 800

Network Source of flow [ns] * h [hour of flow] < = 3500

Or if nsΣ24i=1 h >= L

nsΣ24i=1 h <= M

ns > 0

Valve Constraint

Valves can be closed

Network Valve1 rate of flow [nv1] * h [hour of flow] > = 500

Network Valve1 of flow [nv1] * h [hour of flow] < = 1500

Network Valve2 rate of flow [nv2] * h [hour of flow] > = 200

Network Valve2 of flow [nv2] * h [hour of flow] < = 1000
nv1, nv2 >=4

Pump Constraint

Pump Run [np, h] >= 2

Tank Constraint

Final Volume of Tank = Initial Volume of Tank +/- Gap

Tank Level_CW

tlcwΣ24i=1 h >= L

Where tlcw is level of ClearWell tank 

tlcwΣ24i=1 h <= M

tlcw_inΣ24i=1 h <= tlcw_fΣ24i=1 h +/- final_gap
This is a test.

