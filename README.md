# mf821group11

## TODO:
- Integrate scanner with trade algo. (approx. 3-5 days)
- Test trade algo using real market data during market hours. (N/A)
- Find a way for algo to run on market open w/o human interaction & disconnect from TWS API on market close OR when all trades have been placed. (approx. 2 days)
- Find a way to grab top 5 stocks from scanner and run 5 threads (one thread per stock) (approx. 1 day)
- Terminate thread socket upon completion of bracket order. (approx. 2 hours)
- What to do with our positions that don't sell by EOD? Open to discussion on this one. (N/A)
- Actually test algo on proper triangle conditions (modify as needed), right now it only has a simple, naive, if statement to check if it meets certain criteria. (N/A)


## Blockers :(
None for now :)

## Breakthrough!
Capable of Buying + Selling a stock picked by scanner! HUDI was one of 5 picked by scanner, bought and sold all 3,000 shares. (filed: 11/3)

<img width="635" alt="Screen Shot 2022-11-03 at 6 51 23 PM" src="https://user-images.githubusercontent.com/29446974/199850346-4a2f1e13-749c-499a-a572-dd3fd627f33d.png">

Capable of creating a proper bracket order in that algo will automatically place in 1 buy, and a stop/limit condition. Algo will then automatically transmit and fill the buy order, and wait for price to hit stop/limit conditions, then fill the sell order. (filed 11/4)

<img width="812" alt="Screen Shot 2022-11-04 at 2 38 52 PM" src="https://user-images.githubusercontent.com/29446974/200052541-ae66aa9f-3723-4b64-bafb-712e0d9e6ce1.png">


## DONE:
- add sleep functionality to market scanner. Currently user has to wait at least 30 seconds before typing in a "y/n" response - if user repeatedly prompts for "n" then code errors out as it is trying to pop from an empty queue. Sleep functionality for approx. 32 seconds means that it wil only prompt user after new stocks have been added from the scanner. (approx. 2 hours)
- Bug-1: During trading hours, bars do not get updated during the historical data catchup. This might be due to how the **realtime** flag is being initialized and/or set (approx. 2 hours)(filed 10/28, fixed 10/31)
- Bug-3: When conditions are met for creating a new Bar object, as in when triangle criteria is met, initialization of Bar object fails, since there is no current implicit construction of the Bar object. Potential solution: modify Bar class to have constructor that will implicitly create **Bar.attribute** set to 0 (approx. 1 hour)(filed 10/31, fixed 11/1)
- Bug-5: We get error "can't subtract offset-naive and offset-aware datetimes" whenever a certain code block is ran during market hours. Unsure what line breaks it. Might be related to Bug-4. (approx. 1 hour)(filed 11/1, fixed 11/1)
- Bug-4: We get error "time data '1667310275' does not match format '%Y%m%d %H:%M:%S'" whenever a certain code block is ran during market hours. Unsure what line breaks it. Might be related to Bug-5. (approx. 1 hour)(filed 11/1, fixed 11/1)
- Bug-7: Only parent order in bracket is ever executed, child orders (sell orders) are never executed yet they are properly instantiated. Potential solution is to use ib.sleep(5), but ib_insync is buggy. Might be related to Bug-6. (approx. 4 hours)(filed 11/1, fixed 11/3)
  * Solution: calculate orderIds properly using self.ib.nextValidOrderId
 - Capable of Buying
 - Bug-8: which would mean trader doesn't need to tell TWS to begin filling orders
 - Bug-10: I following the error on almost all orders (ones that do not have this get placed in brackket order). Is this due to quantity (1 vs. 5 vs. 500 vs. 30000 shares bought?) or due to the spread between the profitTarget and stopLoss (do we reduce or increase this spread?)(filed 11/4)
 
```
TWS Error Code:  110
Message for Error Code:  The price does not conform to the minimum price variation for this contract.
```

- Bug-8: So far, no BUYs or SELLs will be filled unlesss user presses "Transmit" button in TWS - unsure if this is intended functionality or a bug. Look at screenshot below for behavior. (aprrox. 3 hour)(filed 11/3)
<img width="718" alt="Screen Shot 2022-11-03 at 6 41 15 PM" src="https://user-images.githubusercontent.com/29446974/199848272-92b24c5d-5505-4212-b87e-f6795eb356a2.png">

- Bug-6: Looks to be that only the first order of the day is properly placed in that it is bought, and appropriately sold (this could be due to a threading socket or orderId issue). All subsequent trades of the day are only ever bought, never sold. Please view below screenshot for behavior. (approx. 4 hours)(filed 11/1)
<img width="865" alt="Screen Shot 2022-11-01 at 4 01 56 PM" src="https://user-images.githubusercontent.com/29446974/199340233-e71c767b-f8cb-4a47-b7d8-f5fde237912d.png">

- Bug-7: Only parent order in bracket is ever executed, child orders (sell orders) are never executed yet they are properly instantiated. Potential solution is to use ib.sleep(5), but ib_insync is buggy. (approx. 4 hours)(filed 11/1, modified 11/3)
  * Potential solution: I used time.sleep() and it appeared to work?
  * Bug is still present, but BUY+SELL pair only ever occurs in around 20% of the time, error message is due to contract not meeting the minnimum price requirement. 


## Backlog:
- Bug-2: Flaky **minutes_diff** computation in that occasionally the difference between time.now() and the time of the retrieved bars is a negative value (this should never happen)(filed 10/31)
  * Ignore this bug for now, it doesn't affect intended functionality or performance
- Bug-5: Consistently get error "strptime() argument 1 must be str, not int" whenever code runs, but code seems to run as expected as if without errors. Changing argument to str breaks everything, so that's why it has not been changed as error suggests (any idea on why this still works and how to fix it?)(approx. 2 hour)(filed 11/1)
  * Ignore this bug for now, it doesn't affect intended functionality or performance


### High Priority Bugs!
None for now :)

