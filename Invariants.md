# Invariants #

## List of Invariants for this Problem ##
- An approach signal will always precede a depart signal.
- The power will never be interrupted.
- Trains on each track only run in one direction.
- Sensors are working.


## Varying Invariants (based on the example FSM)  ##
- If arms are down, and an arrival signal is received at around the same time as a depart signal is received,
  the arms will not go down for the other train that is approaching, which is an unsafe state.
- Similarly, in the bottom ringing arms up state, and we get an approach before time elapses, the arms will not go
  down for an approaching train.

## Prove Completeness ##

| number | arms_down | alarm_on | northbound_present | southbound_present | north_approach | south_approach | north_depart | south_depart | timer_elapsed | safety_hazard |
|--------|-----------|----------|--------------------|--------------------|----------------|----------------|--------------|--------------|---------------|---------------|
| 0      | 0         | 0        | 0                  | 0                  | 6              | 5              | 16           | 16           | 17            |               |
| 1      | 0         | 0        | 0                  | 1                  | -              | -              | -            | -            | -             | 18            |
| 2      | 0         | 0        | 1                  | 0                  | -              | -              | -            | -            | -             | 18            |
| 3      | 0         | 0        | 1                  | 1                  | -              | -              | -            | -            | -             | 18            |
| 4      | 0         | 1        | 0                  | 0                  | 6              | 5              | 16           | 16           | 0       	  |               |
| 5      | 0         | 1        | 0                  | 1                  | 7              | 5              | 16           | 19           | 13      	  |               |
| 6      | 0         | 1        | 1                  | 0                  | 6              | 7              | 19           | 16           | 14      	  |               |
| 7      | 0         | 1        | 1                  | 1                  | 7              | 7              | 19           | 19           | 15      	  |               |
| 8      | 1         | 0        | 0                  | 0                  | -              | -              | -            | -            | -       	  | 20            |
| 9      | 1         | 0        | 0                  | 1                  | -              | -              | -            | -            | -       	  | 20            |
| 10     | 1         | 0        | 1                  | 0                  | -              | -              | -            | -            | -       	  | 20            |
| 11     | 1         | 0        | 1                  | 1                  | -              | -              | -            | -            | -       	  | 20            |
| 12     | 1         | 1        | 0                  | 0                  | -              | -              | -            | -            | -       	  | 21            |
| 13     | 1         | 1        | 0                  | 1                  | 15             | 13             | 16           | 4            | 17       	  |               |
| 14     | 1         | 1        | 1                  | 0                  | 14             | 15             | 4            | 16           | 17      	  |               |
| 15     | 1         | 1        | 1                  | 1                  | 15             | 15             | 13           | 14           | 17      	  |               |

| number | invariant |
|--------|-----------|
| 16     | An approach signal will always precede a depart signal. |
| 17	 | Timer does not start if we don't have an appoach or departure |
| 18     | If a train is present, the alarm must be on |
| 19     | Depart should only be received when arms are down |
| 20     | If arms are down, alarm must be ringing. |
| 21     | If arms are down, then train is present. |
