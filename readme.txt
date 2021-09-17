
Instances used in An exact solution approach for an electric bus dispatch problem (2021)
Authors: Matias Alvo, Gustavo Angulo, Mathias Klapp

----------------------------------------------------------------------------------------------------------------

Base case instance definition:
- an instance is defined by the tuple (|T|, |C|, |V_0|), where |T| is the number of trips, |C| is the number of
chargers available and |V_0|, which is the number of electric vehicles available
- the values considered are as follows:
    - |T|: values in {150, 200, 250}
    - |C|: values in {1, 2, 3}
    - |V_0|: for a given value of |T|, it is calculated as ceiling(d^max*perc^E), for perc^E with values in
    {0.25, 0.5, 0.75, 1}, where:
        - d^max: minimum number of diesel buses required to cover all trips in set T in absence of an electric
        vehicle fleet
        - perc^E: target percentage of the fleet to be composed by electric vehicles

Sensitivity analysis instance definition
- the number of trips is fixed to |T| = 150
- an instance is defined by (|C|, |V_0|, EVA), where EVA corresponds to the relative size of the battery compared to
the one in used in the base case experiment.
- the values of |C| and |V_0| considered are the same as the ones in the base case instances
- EVA: values in {0.5, 0.75, 1}.  The values of e^min remain unchanged, while e^max is set to the corresponding
values in {60, 80, 100}. This ensures that the new battery size is EVA-times the base case battery size

----------------------------------------------------------------------------------------------------------------

Data description

Trips directory:
- there is one file in the directory corresponding to each quantity of trips (|T|) considered. For example, the
file '150.csv' should be used for all instances with 150 trips
- the first line is a header denoting the parameters listed for each trip, which are:
    - t_j^start: trip j's start time (in minutes)
    - t_j^end: trip j's end time (in minutes)
    - e^j: consumption (in SoC units) for an electric vehicle serving trip j
- each of the next |T| lines corresponds to a specific trip, and is of the form {t_j^start},{t_j^end},{e^j}

constant_parameters.csv:
- lists the parameters which are constant across all instances in the base numerical experiment (e^max is changed in
the sensitivity analysis numerical experiment)
- the first line is a header denoting the parameters listed, which are:
    - e^min: lowest feasible SoC value for an electric vehicle's battery at all times
    - e^max: largest feasible SoC value for an electric vehicle's battery at all times
    - e^end: lowest feasible SoC value for an electric vehicle's battery at the end of the day's operation
    - f: charge rate (in SoC/min) for all chargers
    - p^start: start time (in minutes) of operations for all chargers
    - p^end: end time (in minutes) of operations for all chargers
- the next line shows the corresponding value for each of these parameters

d_max.txt:
- contains an array of the form {|T|: d^max}, which for each number of trips (|T|), returns the minimum number of
diesel buses required to cover all trips in set T in absence of an electric vehicle fleet

initial_SoC_levels.csv:
- the first line is a header denoting the only parameter listed for each electric vehicle (e_i)
- the next 100 lines (one per electric vehicle), lists the initial SoC level of bus i (e_i)
- for an instance with |V_0| electric vehicles available, the first |V_0| lines (excluding the header)
 should be retrieved

