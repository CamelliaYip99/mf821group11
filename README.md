# mf821group11

## TODO:
- Integrate scanner with trade algo. (approx. 3-5 days)
- Test trade algo using real market data during market hours. (N/A)
- Find a way for algo to run on market open w/o human interaction & disconnect from TWS API on market close OR when all trades have been placed. (approx. 6 hours)


## DONE:
- add sleep functionality to market scanner. Currently user has to wait at least 30 seconds before typing in a "y/n" response - if user repeatedly prompts for "n" then code errors out as it is trying to pop from an empty queue. Sleep functionality for approx. 32 seconds means that it wil only prompt user after new stocks have been added from the scanner. (approx. 2 hours)
- Bug-1: During trading hours, bars do not get updated during the historical data catchup. This might be due to how the **realtime** flag is being initialized and/or set (approx. 2 hours)(filed 10/28, fixed 10/31)
- Bug-3: When conditions are met for creating a new Bar object, as in when triangle criteria is met, initialization of Bar object fails, since there is no current implicit construction of the Bar object. Potential solution: modify Bar class to have constructor that will implicitly create **Bar.attribute** set to 0 (approx. 1 hour)(filed 10/31, fixed 11/1)
- Bug-5: We get error "can't subtract offset-naive and offset-aware datetimes" whenever a certain code block is ran during market hours. Unsure what line breaks it. Might be related to Bug-4. (approx. 1 hour)(filed 11/1, fixed 11/1)
- Bug-4: We get error "time data '1667310275' does not match format '%Y%m%d %H:%M:%S'" whenever a certain code block is ran during market hours. Unsure what line breaks it. Might be related to Bug-5. (approx. 1 hour)(filed 11/1, fixed 11/1)




## Backlog:
- Bug-2: Flaky **minutes_diff** computation in that occasionally the difference between time.now() and the time of the retrieved bars is a negative value (this should never happen)(filed 10/31)
- Bug-5: Consistently get error "strptime() argument 1 must be str, not int" whenever code runs, but code seems to run as expected as if without errors. Changing argument to str breaks everything, so that's why it has not been changed as error suggests (any idea on why this still works and how to fix it?)(approx. 2 hour)(filed 11/1)


### High Priority Bugs!
- Bug-6: Looks to be that only the first order of the day is properly placed in that it is bought, and appropriately sold (this could be due to a threading socket or orderId issue). All subsequent trades of the day are only ever bought, never sold. Please view below screenshot for behavior. (approx. 4 hours)(filed 11/1)
<img width="865" alt="Screen Shot 2022-11-01 at 4 01 56 PM" src="https://user-images.githubusercontent.com/29446974/199340233-e71c767b-f8cb-4a47-b7d8-f5fde237912d.png">



- Bug-7: Only parent order in bracket is ever executed, child orders (sell orders) are never executed yet they are properly instantiated. Potential solution is to use ib.sleep(5), but ib_insync is buggy. Might be related to Bug-6. (approx. 4 hours)(filed 11/1)

