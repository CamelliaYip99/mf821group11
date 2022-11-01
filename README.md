# mf821group11

## TODO:
- Integrate scanner with trade algo. (approx. 3-5 days)
- Test trade algo using real market data during market hours. (N/A)
- Find a way for algo to run on market open w/o human interaction & disconnect from TWS API on market close OR when all trades have been placed. (approx. 6 hours)


## DONE:
- add sleep functionality to market scanner. Currently user has to wait at least 30 seconds before typing in a "y/n" response - if user repeatedly prompts for "n" then code errors out as it is trying to pop from an empty queue. Sleep functionality for approx. 32 seconds means that it wil only prompt user after new stocks have been added from the scanner. (approx. 2 hours)
- Bug-1: During trading hours, bars do not get updated during the historical data catchup. This might be due to how the **realtime** flag is being initialized and/or set (approx. 2 hours)(filed 10/28, fixed 10/31)
- Bug-3: When conditions are met for creating a new Bar object, as in when triangle criteria is met, initialization of Bar object fails, since there is no current implicit construction of the Bar object. Potential solution: modify Bar class to have constructor that will implicitly create **Bar.attribute** set to 0 (approx. 1 hour)(filed 10/31, fixed 11/1)




## Backlog:
- Bug-2: Flaky **minutes_diff** computation in that occasionally the difference between time.now() and the time of the retrieved bars is a negative value (this should never happen)(filed 10/31)
- Bug-4: We get error "time data '1667310275' does not match format '%Y%m%d %H:%M:%S'" whenever a certain code block is ran during market hours. Unsure what line breaks it. Might be related to Bug-5. (approx. 1 hour)(filed 11/1)
- Bug-5: We get error "can't subtract offset-naive and offset-aware datetimes" whenever a certain code block is ran during market hours. Unsure what line breaks it. Might be related to Bug-4. (approx. 1 hour)(filed 11/1)
