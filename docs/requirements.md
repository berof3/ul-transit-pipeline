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

## Why these questions matter

### Q1: It answers if the service is getting better or worse
### Q2: Shows where delays affect the most trips
### Q3: It will help the UL planner to improve customers experience during those times. Tries to show where and when, not the cause; the cause might be capacity, traffic, or boarding time. Our data can show that delays rise at peak, but not why.
### Q4: It shows if the whether is the reason that makes the busses late. The UL planner can plan for it if the reason weather given that weather is predicatable a few days ahead, so the delay becomes predictable too. Also, if the weather is not the reason that will give us a finding that the delays are driven by something else, like traffic or rush hour
### Q5: This one will keep the whole picture honest. Given that a cancelled departure has no delay, if we only measure average delay, cancellations would quietly disappear from the KPIs and make punctuality look better than it is