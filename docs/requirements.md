# Phase 1: Analytical Requirements

## Project question
Is UL (Uppsala) public transport on time, and does weather make it worse?

## Delay categories
Delay = realtime departure time − scheduled departure time (last observation before departure).

| Category | Delay |
|---|---|
| Early | < −1 min |
| On time | −1 to +3 min |
| Late | > +3 min |

## Analytical questions

| # | Question | Metric | Grain | Data fields needed |
|---|---|---|---|---|
| 1 | Punctuality share per line, week to week | on_time / all departures | line × week | line, trip ID, stop, scheduled time, realtime time |
| 2 | Departures per hour, weekday 07–09 | count(distinct trip) / hours in window | line × date × hour | line, trip ID, scheduled time |
| 3 | Average delay, rush vs off-peak | avg(realtime − scheduled) by period | line × date × hour | line, scheduled time, realtime time |
| 4 | Punctuality vs rain, snow, cold | punctuality share by weather bucket | date × hour | departure fields + SMHI: station, observation time, temperature, precipitation |
| 5 | Cancellation share by line and weather | cancelled / all departures | line × date × hour | line, cancelled flag, scheduled time, weather |
