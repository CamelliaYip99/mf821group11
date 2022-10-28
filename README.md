# mf821group11

## TODO:
- Integrate scanner with trade algo. (approx. 3-5 days)
- Test trade algo using real market data during market hours. (N/A)
- Find a way for algo to run on market open w/o human interaction & disconnect from TWS API on market close OR when all trades have been placed. (approx. 6 hours)


## DONE:
- add sleep functionality to market scanner. Currently user has to wait at least 30 seconds before typing in a "y/n" response - if user repeatedly prompts for "n" then code errors out as it is trying to pop from an empty queue. Sleep functionality for approx. 32 seconds means that it wil only prompt user after new stocks have been added from the scanner. (approx. 2 hours)
